---
title: Print related stored stashes when checkouting a branch
description: "Git one-liner to print related stashes entries just after switching a branch"
dropcaps: true
date: 2018-04-12
published: true
edited: true
comments: https://www.reddit.com/r/git/comments/8budlv/git_alias_to_print_related_stashes_when/?st=jfx3yhf1&sh=e48c9f6c
tags:
- git
- unix
---
I use git stashes parsimoniously and generally prefer to do a _WIP_ commit when I must leave a 
branch. Yet, sometimes, when I struggle to find a good implementation, I cannot resolve myself to 
commit the code -even as a WIP- and prefer to stash it away.  
So git stashes are places where I put my half-baked attempts for an hypothetic later use.

As soon as I checkout a branch, I call `git log` to get back into the swing, if 
the top commit is labelled as _WIP_, I soft reset it and am right back to work. 
Checking available stashes on checkout is not as natural for me and I forget to do it half the time 
thus losing the code stashed or wasting my time rewriting it :sob: ... 

I figured today that I could use the fact that default stashes messages are of the form 
*"WIP on `<branchname>`:"* to grep them just after performing a checkout.
That gave birth to my `.gitconfig` `co` alias :

    co = "!f() { git checkout \"$@\" && git stash list | grep \"$1:\"; }; f"

... and gives following display :

    $ git co master
    Switched to branch 'master'
    Your branch is up-to-date with 'origin/master'.
    stash@{0}: WIP on master: c35edf60 add Curriculum vitae redirect
    stash@{2}: WIP on master: 0977c37 Move <head></head> outside head.html

Tadaam! No more excuses to let stashes rot.  
