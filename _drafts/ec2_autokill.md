---
title: Autokill detached anonymous EC2 instances 
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
the faculty of performing itself an hara-kiri wired as a cron job. The question then becomes : 
How do we detect when an instance get detached? ... When its assigned group name get null.

So here is the script we now ship in the AMI and thet cron calls on an hourly basis :


