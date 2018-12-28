---
title: Cron jobs execution monitoring in slack
description: Small bash wrapper using slacktee to report cron jobs fails to slack
dropcaps: false
published: true
comments: 
tags:
- slack
- unix
---

This post is in the same vein than the [previous one](http://kray.me/2018/09/celery_monitoring_in_slack/) 
but applies to cron jobs instead of celery tasks.  
I used to redirect stderr to a log file for my cron jobs but it took me weeks to figure the jobs were 
crashing in the first place.  
So now I want my jobs to crash loudly, for that purpose I use [slacktee](https://github.com/coursehero/slacktee) util
that posts stdin to slack.

~~~ shell
#!/bin/bash

# Take a command to run in argument. Posts stderr to slack if it fails. 
runcheck() {
    ERR="$($@ 2>&1 > /dev/null)"
    if [ $? -ne 0 ]; then
         echo "\`${1##*/}\` failed" | /usr/local/bin/slacktee.sh -p -u "$HOSTNAME" --config /home/ubuntu/.slacktee-alert
        if [ ! -z $ERR ]; then
             echo "${ERR}" | sed -e 's/^/>/' | /usr/local/bin/slacktee.sh -p -u "$HOSTNAME" --config /home/ubuntu/.slacktee-alert
        fi
    fi
}

main() {
    runcheck $@
}
main $@
~~~ 
<span class='buffer-title center'>runcheck.sh</span>

So my cron tasks are declared like so :

~~~plaintext
$ crontab -l
SHELL=/bin/bash

# 0 */2 * * * /home/ubuntu/bin/runcheck.sh /home/ubuntu/my_project/binaries/cron/run_critics.sh
~~~

In case of failure, a slack alert pops with all needed infos : hostname, command that fails and error message.

{:.center}
![slack notification with developers facemojis](/public/img/posts/cron_alert.png) 
