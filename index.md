---
layout: default
title: "Ex commito: Kraymer technical blog about Open source, Python, Git, Jekyll, etc"
description: "My blog is a vitrine to my open source work : I document projects from the past, write
a post when I release new stuff and track my future projects."
redirect_from: 
- /blog
- /r
---

<div class="blog-index">
  {% assign post = site.posts.first %}
  {% assign previous-post = site.posts[1] %}
  {% assign content = post.content %}
  {% assign date = post.date %}
  {% include {{post.layout}}.html post=post previous-post=previous-post %}
  {% include related.html post=post %}
</div>
