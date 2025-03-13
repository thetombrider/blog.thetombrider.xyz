---
layout: page
title: Notes
permalink: /notes/
---

This page is rendered dynamically and includes all my notes.

{% for post in site.tags.notes %}
    <div class="post">
        <h2><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h2>
        <span> - {{ post.date | date: "%B %d, %Y" }}</span>
    </div>
{% endfor %}