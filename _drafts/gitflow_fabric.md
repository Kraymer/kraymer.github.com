---
title: Gitflow deployment strategy with fabric
dropcaps: false
published: true
draft: true
tags:
- python
---

~~~
fab release:version=X.Y.Z `(locally)`
├── release_freeze `(locally)`
│   │ + check no tag exist for given version, if one 
│   │   exist, asks if we continue (y/n)
│   │ + check tag is direct successor of last one
│   │ + check if TODOS have been inserted in release 
│   │   commits, if some exist asks if we continue (y/n)
│   │ + exit if repo is not clean (unless force=True)
│   │ + open nano editor to show release changelog 
│   │   ONGOING.md for last minute edits
│   │ + copy release changelog from ONGOING.md to CHANGELOG.md
│   │ + commit CHANGELOG.md
│   │ + git push branch
│   │ + git checkout master; git merge branch
│   │ + check that master and branch are synchronized using 
│   │   `git diff`. Exit if not in sync.
│   └ + push to origin 
│                                  
├── deploy:version=X.Y.Z  `(on DEPLOY server)`
│   │ + git pull master branch
│   │ + git tag vX.Y.Z
│   │ + check that no uncommited migration, if one exist, asks 
│   │   if we continue (y/n)
│   │ + send 'deploy start' slack notification
│   ├── prepare_deb()   
│   │   │ + collect statics
│   │   └ + create .deb with `fpm` tool
│   ├── upload_deb_to_S3()
│   ├── deploy_deb()   `(on EC2 instances)`
│   │   │+ download deb
│   │   └+ install deb with dpkg
│   ├── generate_ami()    `(on AMI server)`
│   │    Dl, install .deb, make ami and set autoscalers with it so 
│   │    that launched EC2 instances are always up-to-date and don't 
│   │    have to install last deb on startup.
│   ├── manage.py migrate()
│   ├── git push tag 
│   ├── release_merge
│   │    Synchronize hotfix/master/develop branches (gitflow)
│   ├── sudo supervisorctl restart all
│   └ send 'deploy end' slack notification
└           
~~~
