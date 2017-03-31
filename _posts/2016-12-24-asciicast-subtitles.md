---
layout: post
title: Add live key pressed overlay to your asciicasts with keyriban
published: false
comments: true
tags:
- open-source
- python
header:
  overlay_image: /assets/images/lena_river1.jpg
---
Asciicast elegant text-based approach has huge benefits, enabling copy-paste being the first.  
Yet, with no guiding voice track, the viewer comprehension of what happens on screen is seriously hampered.  
What textual bits of information can we inject in the recording to make it clearer ?

## Typing comments to give context information

### Inlined shell comments

Use shell comments to introduce what next command will do. That is the technique used on the [asciicast homepage demo](https://asciinema.org/a/42383).    
Make appropriate use of inline comments to answer potential interrogation the viewer may have.
    
{% highlight bash %}
    # accounts.csv is a Gnucash export of my accounts
    head -n 2 ./accounts.csv 
    # qifacc populate ~/.qifqif.json categories file from csv list of accounts 
    qifacc a ccounts.csv 3  # extract the 3rd column
{% endhighlight %}

I recommend [zsh shell syntax highlighting package](https://github.com/zsh-users/zsh-syntax-highlighting) that helps bring out comments from instructions.

### Tmux comments panel 

We need another input method to comment on curses application, when shell prompt is not always available.  
Using tmux, we'll split the window vertically and configure a 2 rows thick panel with a background color to make it pop out. 

    # test
    tmux.conf
    
Simply click the panel and type your text to comment on actions that are undertaken in the main tmux panel.  

I have experimented with displaying text slides in the comments panel, using a program like patat.  
I decided to ditch that approach for two reasons :  

  - pre-written slides authorize no mess-up during recording. I prefer free comment and the a part of improvisation that goes with it.
  - typing comments attracts the viewer eye better than turning slide does. Plus the longer time needed to type the text, give 
    watcher enough time to read it. 

### Displaying key presses 

