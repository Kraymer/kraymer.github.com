---
title: Pruning beets genre canonicalization tree
published: true
date: 2012-10-13
tags:
- beets
- music-management
- open-source
- python
redirect_from: /blog/customizing-beet-genres-canonicalization-tree
---

Unlike most tags, 'genre' accept some latitude and is open to interpretation. In others words: a music management nightmare.
The [hundreds variations of genres][3] in the nature are too numerous to be exploited for classification purposes. You gotta restrict yourself!

**Figure a limited set of genres that fits your music tastes**. Focus on genres that don't overlap and partition your library into sets of comparable sizes.

Done right, genres are a great asset that enable to browse through files faster and to create better playlists based on genre filtering.

### Genres entrance policy

Once you have handpicked your genres list, the easier way to keep it intact consist in ensuring that new additions to your library don't introduce alien genres.

I use [beets][4] to inject newcomers in my library and bring them into line.

You will have to activate the `lastgenre` plugin : it uses [lastfm][2] crowdsourced data to fetch the genre information. I encourage you to read the [plugin documentation page][1] first. The plugin works great by default, but you must tweak its settings if you want to enforce a strict set of genres.

`beetsplug/lastgenre/genres.txt` is a whitelist of all accepted genres. Replace the default one by
your custom list (all genres lowercase, one genre per line)

`beetsplug/lastgenre/genres-tree.yaml` is the genres canonicalization tree : it stores the genres hierarchically relying on outline indentation for structure. It allows to find multiples candidates from a given genre thus improving the chance to have one present in user whitelist.

![lastgenre plugin canonicalization steps](/public/img/posts/lastgenre_c14n.png)
*An example of lastgenre plugin canonicalization: resolving 'crunk' to 'hip-hop' : lastfm tag tree branch is parsed backward until a tag present in user whitelist is found.*

Edit the yaml file to introduce your genres at strategic places : placing them near the tree root help you maximize the number of suggested genres that are funneled to your accepted tags.

![editing canonicalization tree](/public/img/posts/c14nedit.jpg)
*Diff view of genres-tree.yaml showing changes done to redirect genres to 'hip-hop'.*

[1]: http://beets.readthedocs.org/en/latest/plugins/lastgenre.html
[2]: http://www.lastfm.com
[3]: https://gist.github.com/1241307
[4]: http://beets.radbox.org/

