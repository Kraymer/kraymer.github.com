--- 
layout: note
title: "Downloading magnet links as .torrent files"
published: true
date: 2013-07-15
excerpt: ""
tags:
- misc
---

Since magnets have been introduced in early 2012, **I needed a way to convert a magnet URI to torrent** and found [this tutorial](https://forum.utorrent.com/viewtopic.php?id=115820). It describes an elegant solution relying solely on a browser bookmark, that gets you a torrent file named after the hash of its content.

But having a bunch of torrents files with hexadecimal hashnames sitting in a folder isn't super user friendly : would it be hard to have an evocative name for each file ?  
As a matter of fact, no ... say hi to [**torrefy**](https://github.com/KraYmer/torrefy), the python script that sorts out torrent hash keys.

    $ torrefy.py -v 815F79F2E8B25B3484019887DA40113546CB2935.torrent 
    Renaming 815F79F2E8B25B3484019887DA40113546CB2935.torrent to 
    Scandal.US.S02E18.HDTV.x264-LOL.mp4.torrent    

As usual, I recommend to create an [Hazel](http://www.noodlesoft.com/hazel.php) rule that takes care of unhashifying the name of any freshly downloaded torrent. Enjoy!


![Triggering torrefy.py via an Hazel action](/public/img/posts/hazel-torrefy.png)
