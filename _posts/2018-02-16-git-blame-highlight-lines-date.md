---
title: Highlighting lines in git blame output based on dates
description: "Git one-liner to highlight lines committed at specific date(s) using an ack regex"
dropcaps: true
date: 2018-02-16
published: true
comments: https://www.reddit.com/r/git/comments/7xupht/oneliner_highlight_lines_in_git_blame_output
tags:
- git
- unix
---

I tracked a bug today using `git blame` and had a vague idea when the bug appeared, so I was mostly
interested by changes introduced during the last 30 days.  
Perusing `git blame` output to filter out too old lines was tedious, and so tonight I searched for 
a way to improve the output by highlighting lines in the desired period of time.  
Here is an example, highlighting changes that happened from 2017 onward :

<script src="https://asciinema.org/a/163256.js" id="asciicast-163256" async></script>

The command is thus of the form : 

~~~ shell
git blame FILE | ack --nogroup --passthru '.*(?:DATE_1|...|DATE_N).*?\)'
~~~

Few explanations :
- `passthru` option prints all lines, whether or not they match the expression
- a non capturing group is used `(?:...)` so that the highlight selection matches the whole regex, not just the date group
- we use a lazy quantifier `.*?` to stop the highlighting at the first `)` delimiter, in case the line of code contains some others

As usual, I don't need to remember the exact command, as I rely on my zsh history to autocomplete my typing, or my [git cheatsheet](https://raw.githubusercontent.com/Kraymer/F-dotfiles/master/cheat/.cheat/git) when the history fails me.
