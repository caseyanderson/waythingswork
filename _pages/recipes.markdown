---
title: recipes
permalink: /recipes.html
layout: page
---

<div class="posts">
{% assign sorted-posts = site.posts | where: "categories","recipes" %}
{% for post in sorted-posts %}
  <h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
{% endfor %}
</div>
