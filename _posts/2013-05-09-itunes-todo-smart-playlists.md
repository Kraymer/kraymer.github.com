---
title: Todo playlists
published: true
tags:
- itunes
- music-management
date: 2013-05-09
redirect_from:
- /blog/itunes-todo-smart-playlists/
---

![iTunes screenshot with playlists in sidebar](/public/img/posts/management_playlists.jpg)

As soon as your collection grows much, smart playlists can prove useful to classify the amount of maintenance work that need to be done.  
I use them as auto-generated todo lists for my music: a live listing of the tracks that need to be knocked into line, to make the library aim towards complete sanity :)  
Please find below the six playlists I use and their corresponding correcting actions. 

### *Unsynced ratings* folder

**What?** Songs which have ratings value not backed up by *Grouping* tag.
Five playlists, one for each ratings value.  
*Level one* playlist defined as `Rating` `is` `★☆☆☆☆` AND `Grouping` `is not` `1*`, etc.
  
**Why?** I only trust [resilient ratings][2].  

**Action?** When I rate music on my phone or directly on iTunes, the playlist fills up. Regularly, I purge the folder by selecting all tracks of a group and editing the *Grouping* tag.

### *To ditch*

**What?** Songs which album rating is less than 2 stars.  

**Why?** Remove the weakest albums from my library.  

**Action?** The decision to ditch the album depends on the fact that all the tracks have been rated or not (setting a filter that would consider only completely rated albums cannot be done).  
In any case, the playlist offers good candidates to pick for a *last chance playback* when you're in a mood to lighten your library footprint.

### *To upgrade*

**What?** Quality stuff that would deserve to be reimported at higher bitrate.  
Playlist defined as `Album Rating` `is greater than` `★★★☆☆` AND `Bit Rate` `is less than` `160` kbps.  

**Why?** Because reimporting music is time/money consuming, it makes sense to start by promoting the tunes that I like the most.  

**How?** Once an album to upgrade is spotted, download it at desired bitrate
and use [replica][4] to surreptitiously replace album folder by new one without iTunes even noticing.

### *To rate*

**What?** All unrated songs.  
Playlist defined as `Rating` `is` `<no stars>` AND `Grouping` `does not contain` `*`.   

**Why?** Mostly used as a songs tank for the more-focused *Phone* playlists (see below).  

**Action?**  Make sure that *Live updating* playlist setting is unchecked so playback get not constantly interrupted when you're in a rating session while listening through the playlist.

### *Phone - Auto*

**What?** Recently added songs waiting to be rated.  
Playlist defined as `Date added` `in the last` `3` `months` AND `Playlist` `is` `To rate`.  

**Why?** Since few years, I add only correctly tagged songs into iTunes. 90% of the job is done upstream by [beets][5] but rating is a manual process. Once imported in iTunes, the newcomers are picked up by the system and included in this playlist until they are rated.

**Action?** Sync this playlist with your phone (I use [iSyncr][3] on my android phone).  
Pick the period duration so that it makes a chunk of tracks sized to your whole week transits, ie you should been able to *clear up* the playlist in a week.
Synchronize the playlist every morning and see its size melt like snow in the sun as the number of unrated songs decrease!  
Increase the *Date added* span incrementally as your library get cleaner.

### *Phone - Manual*

**What?** No smart playlist here but a cherry picked selection of songs to rate (taken from *To rate*).

**Why?** I bit off more than I could chew back in the days and I'm now left with a large amount of songs to rate.  
I prefer selecting a handful of songs to listen for a transit journey, rather than having the massive *To rate* playlist synced on my phone.

**Action?** Same as *Phone - Auto* but rated songs must be removed from playlist manually! 
 

[1]:{{ site.baseurl }}{% post_url 2011-09-10-daily-routine-smart-playlist-filterings %} 
[2]:{{ site.baseurl }}{% post_url 2011-03-13-resilient-id3-embedded-ratings %}
[3]:http://www.jrtstudio.com/iSyncr-iTunes-for-Android
[4]:https://pypi.python.org/pypi/replica
[5]:http://beets.radbox.org/
