---
title: briefs
layout: page
permalink: /briefs.html
---

<div class="posts">
    {% assign sorted-posts = site.posts | where: "categories","briefs" %}
    {% for post in sorted-posts %}

        <h3>{{ "Week " | append: post.week}}.{{ post.number }} <a href="{{ post.url }}">{{ post.title }}</a></h3>

{% endfor %}
</div>

