---
title: Deep in F-dotfiles &colon; zsh package
link: https://github.com/Kraymer/F-dotfiles/tree/master/zsh
dropcaps: true
date: 2017-06-26
published: true
edited: true
issue: 11
tags:
- unix
- open-source
---

This post is the first of a serie focused on some cool things stored in
[my dotfiles](https://github.com/Kraymer/F-dotfiles).
The topical organization of my dotfiles is such that each blog post will be dedicated to a given
package. Today we will start with the basics, setup of the shell with the `zsh` package.

    ├── .oh_my.zsh                Zsh theme and plugins
    ├── .zsh
    │   ├── aliases.zsh
    │   ├── config.zsh            Configure shell behavior
    │   ├── dircolors.256dark     Colored ls
    │   └── functions.zsh         Custom shell functions
    └── .zshrc                    Routine loading all .zsh files

### [.oh_my.zsh](https://github.com/Kraymer/F-dotfiles/blob/master/zsh/.oh_my.zsh)

![zsh prompt](/public/img/posts/zshprompt.png)

I use [Oh My Zsh](https://github.com/robbyrussell/oh-my-zsh) for its plugins coupled with
[Powerlevel9k](https://github.com/bhilburn/powerlevel9k) theme that makes the *pimpization* of `PS1`
a treat.

The setup file weights a dozen lines (comments excluded) but has a tremendous impact on my
productivity, which is no surprise given that I spend most of my work day in a shell session.
I can live without the badass prompt, but I feel the pain when I ssh onto servers and lose my
`autojump` and `history-substring-search` plugins superpowers.

I don't use many plugins as I want to keep my prompt snappy, but core zsh is shipped with [a bunch
of powerful features](https://code.joejag.com/2014/why-zsh.html) already.

### [aliases.zsh](https://github.com/Kraymer/F-dotfiles/blob/master/zsh/.zsh/aliases.zsh)

I use custom bash aliases parsimoniously, I prefer to do things the canonical way.
My primary use for aliases is to add default flags that i consider essential to commands like `-c` for `nano`.

But nothing fancy here.

### [config.zsh](https://github.com/Kraymer/F-dotfiles/blob/master/zsh/.zsh/config.zsh)

That's where I put settings relative to shell core functions.
In particular the `history` config is here : the filesize is boosted and the `SHARE_HISTORY` attribute
makes the history work ok with multiple iTerm opened tabs.

I put `TMOUT` setting to `60` seconds so that the hour in my prompt get updated : doing it one per
minute does not distract the eye and means you always have current time in prompt even when you're
idle.

### [functions.zsh](https://github.com/Kraymer/F-dotfiles/blob/master/zsh/.zsh/functions.zsh)

Where things get interesting.
We have `which` and `who` commands but the need for `where` arise much more frequently :

    where() {
        find . -name \*$1\*
    }

But the one function I would bring with me on a desert island is the one wrapping `ssh` command
that attaches me to an existing tmux session once connected.

### [.zshrc](https://github.com/Kraymer/F-dotfiles/blob/master/zsh/.zshrc)

This file is responsible to source all the .zsh files located in my `~/.zsh` directory.
It's useful when you want a dotfiles package to alter an environment variable eg `$PATH`, you just
write a `<package>/.zsh/<package>.env` and reinstall the package via `stow`.

This dynamic sourcing step is what makes F-dotfiles packages installs so seamless.

---

*Any question or insights to share regarding zsh setup ? Please leave a [comment](https://github.com/Kraymer/kraymer.github.com/issues/11).*


