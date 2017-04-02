---
layout: default
---

<div class="blog-index">  
  {% assign post = site.posts.first %}
  {% assign content = post.content %}
  {% assign date = post.date %}
  {% include post.html post=post %}
  {% include related.html post=post %}
</div>
