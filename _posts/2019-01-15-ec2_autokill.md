---
title: Autokill detached anonymous EC2 instances 
description: Save money by stopping EC2 instances as soon as they get detached from autoscaler
dropcaps: true
published: true
draft: true
tags:
- aws
- unix
---
It's not rare to detach an EC2 instance to have access to a server in a production-like environment
or to test how the autoscaler reacts after the sudden loss of an instance, etc.  
It's not rare neither that once you have done your job with the instance, you forget to stop it.
And it runs for days costing you money for nothing.

Until now we have stated the rule at work that "no name & no group name" instances could be stopped 
instantly (so the first thing when working on a detached instance consists to give it a name).  
I decided to automate this, as killing thing is a pet peeve of mine (cf _[ezkill, selective process killing made easy](http://kray.me/2017/03/ezkill-kill-process/)_).  
Rather than having a master instance in charge of executing the detached ones, each instance has 
the faculty of performing itself an hara-kiri wired as a cron job. The instance check its group 
name periodically and when it gets null, it means instance is detached and should shutdown.

So here is the script we now ship in the AMI, called by cron on an hourly basis :

~~~
#!/bin/bash

# This script is executed on an instance itself in order to determine if it is detached.
# If so, it shuts itself down after alerting staff on slack.


INSTANCE_ID=`ec2metadata --instance-id`
IS_LONER_SERVER=`aws ec2 describe-tags --filters Name=resource-id,Values="$INSTANCE_ID" Name=key,Values=Name --query Tags[].Value --output text`
if [ $? -ne 0 ]; then { echo "Failed, aborting." ; exit 1; } fi
IS_AUTOSCALED_SERVER=`aws ec2 describe-tags --filters Name=resource-id,Values="$INSTANCE_ID" Name=key,Values=aws:autoscaling:groupName --query Tags[].Value --output text`
if [ $? -ne 0 ]; then { echo "Failed, aborting." ; exit 1; } fi


if { [ -z "$IS_LONER_SERVER" ] && [ -z "$IS_AUTOSCALED_SERVER" ]; }; then
    echo 'Detached: `shutdown` in 5 minutes.' | /usr/local/bin/slacktee.sh -p -u "$HOSTNAME" --config /home/ubuntu/.slacktee-alert
    sudo shutdown" | at now + 5 minutes
fi
~~~

