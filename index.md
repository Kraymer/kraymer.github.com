---
layout: default
date: 2010-12-18

---

<div class="blog-index">  
  {% assign post = site.posts.last %}
  {% assign content = post.content %}
  {% assign date = post.date %}
  {{ post.date }}
  {% include post_detail.html %}
</div>
