---
title: "Django: check for uncommited migrations on deploy"
description: "Small check to integrate into your fabric deployment"
dropcaps: false
published: true
comments: https://www.reddit.com/r/django/comments/8iysf4/check_for_uncommited_migrations_on_deploy/
tags:
- django
- python
---
Small check to integrate into your fabric deployment method. It detects uncommited migrations and 
prompt user to continue or abort the deployment.

```python
from fabric.api import local

def check_migrations():
    """Return true if no migration file left uncommited"""
    mig = local('./manage.py makemigrations', capture=True)
    if mig.split()[0] != 'No':  # No changes detected
        local('git clean -f')   # Cleanup generated migrations
        print(mig)
        ok = raw_input('\nUncommited migration(s). Continue? [y/n]')
        if ok.lower() != 'y':
            return False
    return True
```
