---
layout: default
title: "Kraymer technical musings: Open source, Python, Jekyll..."
redirect_from: /blog
---

<div class="blog-index">
  {% assign post = site.posts.first %}
  {% assign previous-post = site.posts[1] %}
  {% assign content = post.content %}
  {% assign date = post.date %}
  {% include {{post.layout}}.html post=post previous-post=previous-post %}
  {% include related.html post=post %}
</div>
