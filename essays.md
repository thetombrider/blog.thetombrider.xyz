---
layout: page
title: Essays
permalink: /essays/
---

This page is rendered dynamically and includes all my essays.

{% assign notes_posts = site.posts | where: "tags", "essays" %}
{% for post in notes_posts %}
    <div class="post">
        <h2><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h2>
        <span> - {{ post.date | date: "%B %d, %Y" }}</span>
    </div>
{% endfor %}

