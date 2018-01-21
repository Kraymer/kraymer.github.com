---
title: Blog last publish date in favicon
dropcaps: true
date: 2018-01-21
published: true
edited: true
tags:
- jekyll
- open-source
---

As for every details of [*Ex commito* theme](https://github.com/Kraymer/kraymer.github.com), I wanted the favicon to convey the maximum of information.
Basing your favicon on a thumbnail of your homepage sounds like a pretty dumb idea at first.  
Obviously abstracting parts of the page details is essential to make the 128x128 square legible : I kept just the vertical split with artsy colourful sidebar and creamy right side. 

{:refdef: style="text-align: center;"}
![empty favicon](/public/img/favicon.png)
*Favicon empty background*
{: refdef}

That's a gross preview of how the blog looks, but that does not bring any useful information and makes a shitty favicon for sure.  
But put the date of your last post in the empty right part of the image and this icon becomes a thing of beauty, *erm*. The last publishing date identifies the state of the website like no other (metric). 

Because we don't have that much space available we use the short `MMDD` format to print the date. 

<script src="https://gist.github.com/Kraymer/d014b40303dbfa4dda423efe5dba7a01.js"></script>

This script generates the 365 different versions of the icon to cover the whole year, for a total size of 4,3M.

And to use the correct version of the favicon, just use these lines in head.html :

<script src="https://gist.github.com/Kraymer/83a83592711b1d9967b2c4f30a56621a.js"></script>

Have a look in your browser tab for the result! :sparkles:
