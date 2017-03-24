---
layout: default
---

<div class="blog-index">  
  {% assign post = site.posts.last %}
  {% assign content = post.content %}
  {% assign date = post.date %}
  {% include post.html post=post %}

</div>
