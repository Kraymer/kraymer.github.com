---
title: Blog last publish date in favicon
description: "Tutorial for your jekyll static blog: display date of last published post in your favicon image. Pregenerate 365 favicons using imagemagick."
dropcaps: true
date: 2018-01-21
published: true
comments: https://www.reddit.com/r/Jekyll/comments/7rwr7c/how_to_put_your_blog_last_publish_date_in_favicon/
tags:
- jekyll
- open-source
---

As for every details of [*Ex commito* theme](https://github.com/Kraymer/kraymer.github.com), I wanted the favicon to convey the maximum of information.
Basing your favicon on a thumbnail of your homepage sounds like a pretty dumb idea at first.  
Obviously abstracting parts of the page details is essential to make the 128x128 square legible : I kept just the vertical split with artsy colourful sidebar and creamy right side. 

{:.center}
![empty favicon](/public/img/favicon.png)  
*Favicon empty background*

That's a gross preview of how the blog looks, but that does not bring any useful information and makes a shitty favicon for sure.  
But put the date of your last post in the empty right part of the image and this icon becomes a thing of beauty, *erm*. The last publishing date identifies the state of the website like no other (metric). 

Because we don't have that much space available we use the short `MMDD` format to print the date. 

~~~ python
import os
from PIL import Image, ImageDraw, ImageFont

# Generates timestamped favicon images for every day of the year, store images in 12 folders (one per month).

FONT = ImageFont.truetype(os.path.abspath(os.path.join('static', 'fonts', 'Avenir Next Condensed.ttc')), 60)

for month in [str(x).zfill(2) for x in range(1, 13)]:
    os.makedirs(month)
    for day in [str(x).zfill(2) for x in range(1, 32)]:
        img = Image.open('public/img/favicon.png')
        canvas = ImageDraw.Draw(img)
        canvas.text((65, 50), (str(day).zfill(2)), font=FONT, fill=(165, 85, 64))
        canvas.text((65, 0), (str(month).zfill(2)), font=FONT, fill=(165, 85, 64))
        img.save(os.path.join('%s/favicon_%s.png' % (month, day)))
~~~

This script generates the [365+ different versions](https://github.com/Kraymer/bulkdata/tree/master/excommito) of the icon to cover the whole year, for a total size of 4,3M.

And to use the correct version of the favicon, just use these lines in `head.html` :

{% raw %}
~~~ liquid
{% capture last_date %}{{ site.posts.first.date }}{% endcapture %}
<link rel="shortcut icon" type="image/png" 
href="https://raw.githubusercontent.com/Kraymer/bulkdata/master/excommito/{{ last_date | slice: 5,2 }}/favicon_{{ last_date | slice: 8,2 }}.png">
~~~
{% endraw %}

Have a look in your browser tab for the result! :sparkles:
