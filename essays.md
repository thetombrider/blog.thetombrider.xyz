---
layout: page
title: Essays
permalink: /essays/
---

This page is rendered dynamically and includes all my essays.

{% for post in site.tags.essays %}
    <div class="post">
        <h2><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h2>
        <span> - {{ post.date | date: "%B %d, %Y" }}</span>
    </div>
{% endfor %}