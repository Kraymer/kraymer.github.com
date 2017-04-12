---
layout: default
---

<div class="blog-index">  
  {% assign post = site.posts.first %}
  {% assign previous-post = site.posts[1] %}
  {% assign content = post.content %}
  {% assign date = post.date %}
  {% if post.layout == "note" %}
    {% include note.html post=post previous-post=previous-post %}
  {% else %}
    {% include post.html post=post previous-post=previous-post %}
  {% endif %}
  {% include related.html post=post %}
</div>
