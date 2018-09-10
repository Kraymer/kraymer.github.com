---
title: Slackery
description: Celery tasks execution monitoring in slack
dropcaps: false
published: true
tags:
- python
- slack
---

> */sla-kuh-ree/*  
>     1. the act of engaging in unproductive activities   
>     2. the act of monitoring celery processes via slack  

We will detail in this post how to have a slack notification when a celery task is being executed.    
This is something I wrote to circumvent the blindness I had about monitoring the proper execution 
of tasks, as accessing the queues list with `rabbitmqctl` was immediatley overwhelming because of 
the number of tasks involved.

Here how looks notifications for tasks decorated with `@slackery` decorator : 
![](/public/img/posts/slackery_notif.png)

First, if not done already, you must configure your celery app with dedicated settings to be able 
to distinguish whether a function is called from webserver or a celery process :

~~~ python
import socket
from jelouemoncampingcar.settings import * # NOQA

IS_CELERY = True
HOSTNAME = socket.gethostname()
~~~ 
<span class='buffer-title center'>celery_settings.py</span>

We can now write our decorator :  
- check first that `IS_CELERY` is defined
- if so, send a message to slack channel webhook url with current time and instance hostname

~~~ python
from functools import wraps
from django.utils import timezone
from utils.slack import slack_notify

def slackery(fun):
    """
    Post slack notification when celery task is executed
    """
    @wraps(fun)
    def wrapper(*args, **kwargs):
        if getattr(settings, 'IS_CELERY', False):
            slack_notify('celery', '%s Executing %s' % (str(timezone.now())[:-7], fun),
                title=settings.HOSTNAME)
        return fun(*args, **kwargs)

    return wrapper
~~~

And if you think the celery icon on the screenshot above is yummy, you can get it 
[here](http://www.iconhot.com/icon/pickin-time/celery.html).
