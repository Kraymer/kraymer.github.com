--- 
layout: post
title: Exporting music from Itunes (Mac) while keeping source folders arrangement
published: true
date: 2010-12-18
tags: 
- itunes
- music-management
redirect_from: /blog/exporting-music-from-itunes-mac-while-keeping/
---
Thanks to smart playlists in *iTunes*, you can build a playlist gathering the best songs of your library in few seconds. I recently had to copy a such *best of* selection to an external hard drive. A simple drag & drop from *iTunes* to the *Finder* can do the trick, yet resulting in a mess of unrelated files now all located in the same directory.  
So, what is the easiest way to copy a playlist content to a specified location and have the folders arrangement of your source files duplicated on your destination drive ?

Here is the solution that I've reached, unfortunately it involves no less than 3 different steps.

### Export the playlist to M3U file

Because it can't be done directly in *iTunes*, you have to export your playlist first.
Select your playlist and right click *Export* then choose the M3U8 format. M3U export has been added *recently* to *iTunes* (in one of the 9.x release), so upgrade your *iTunes* if the only choices you&rsquo;re faced with are text and xml.

### Fix the M3U file

*iTunes* saves M3U files using DOS/Windows newlines, fire up your *Terminal.app* to correct that :

```bash
tr '\r' '\n' < input_m3u
```

### Transfer files using *cpio* command

*cpio* is the perfect tool to copy files listed in the M3U. Run it with *-dp* options to activate pass-through mode and automatic directories creation :

```bash
tr '\r' '\n' < input_m3u | cpio -pd  destination_directory > m3u_file
```


Voilà ! All files are copied to destination and the directories structure is preserved which is neat when you sort your files by artists or year, etc.  

<iframe src="http://www.youtube.com/embed/1N5vNI1ISUc?wmode=transparent" allowfullscreen frameborder="0" height="417" width="500"></iframe>
