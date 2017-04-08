---
layout: default
---

<div class="blog-index">  
  {% assign post = site.posts.first %}
  {% assign previous-post = site.posts[1] %}
  {% assign content = post.content %}
  {% assign date = post.date %}
  {% include post.html post=post previous-post=previous-post %}
  {% include related.html post=post %}
</div>
