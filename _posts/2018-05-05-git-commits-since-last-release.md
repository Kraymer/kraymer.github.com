---
title: "Git one-liner: show commits since last release"
description: "Git one-liner to show all commits that happened since last tag"
dropcaps: false
date: 2018-05-05
published: true
edited: true
tags:
- git
- unix
---
This git one-liner is useful for checking there is no omission in the changelog before shipping a 
release. 

~~~ shell
alias git-log-since-rlz='git log --oneline --pretty=format:"%h%x09%an%x09%s" --no-merges `git describe --abbrev=0 --tags`..HEAD'
~~~

And you get a no fluff view of the commits that happened since last tag :

```plaintext
$ git-log-since-rlz
c5bf39db        Fabrice Laporte add new post 2018-05-03-slack_deploy_notifications.md
b047232e        Fabrice Laporte use terminal styling from mademistakes
fed1d2c5        Fabrice Laporte add comments link to last post
a9f137a7        Fabrice Laporte publish 2018-04-16-terminal_css.md
1335bd76        Fabrice Laporte Remove unpublished post
```


