--- 
layout: post
title: "ezkill, selective process killing made easy"
published: true
edited: true
date: 2017-03-29
excerpt: ""
tags:
- open-source
---
`killall` and `pkill -f` are the two most popular tools to send SIGTERM to all 
processes running a specified command.
With [**`ezkill`**](https://github.com/Kraymer/ezkill) I want to provide more 
flexibility in the choice of processes to terminate while honoring the terse
efficiency of aforementioned commands.

**`ezkill`** list processes matching input pattern, `ps` style, 
and add a letter prefix before each line. 
This single letter plays the role of pid, you designate which processes to kill 
by entering their letters at the prompt. 

<script type="text/javascript" src="https://asciinema.org/a/5dxi20xzerjxhw2fn1tdhqi47.js" id="asciicast-5dxi20xzerjxhw2fn1tdhqi47" async></script>

So that's the trade-off: only the 26 first matching processes are displayed, 
only one keystroke per process to kill is required. 
