---
title: Custom css style for terminal codeblocks
dropcaps: false
published: true
link: https://github.com/Kraymer/kraymer.github.com/commit/c722663
comments: https://talk.jekyllrb.com/t/custom-css-style-for-terminal-codeblocks/1703
tags:
- jekyll
---

I just added [dedicated css code](https://github.com/Kraymer/kraymer.github.com/commit/c722663) to render terminal sessions on *Ex commito*, rather than relying on 
markdown fenced code blocks.  
So now these terminal blocks stand out from code blocks and it improves articles readability at 
first sight.

I use a black background with a thin green margin to evocate the _hacker color scheme_ as seen in the movies :

<terminal>
$ jekyll --help <br>
jekyll 3.7.0 -- Jekyll is a blog-aware, static site generator in Ruby <br>
<br>
Usage: <br>
<br>
jekyll &lt;subcommand&gt; [options] <br>
</terminal>

Whereas code excerpts use the solarized dark theme :

~~~ html
<terminal>
$ jekyll --help <br>
jekyll 3.7.0 -- Jekyll is a blog-aware, static site generator in Ruby <br>
<br>
Usage: <br>
<br>
jekyll <subcommand> [options] <br>
</terminal>
~~~

Unlike markdown fenced code blocks, I must manually insert `<br>` markups at the end of each line 
in the `<terminal>` div, but it's overall a small price to pay.


