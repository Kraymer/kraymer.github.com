---
title: Slackery
description: Celry tasks execution monitoring in slack
dropcaps: false
published: false
draft: True
tags:
- python
- slack
---
I will detail on this post how to have a slack notification when a celery task is being executed.    
This is something I wrote to circumvent the blindness I had about monitoring the proper execution 
of tasks as accessing the queues list with `rabbitmqctl` was immediatley overwhelming because of 
the number of tasks involved.  

