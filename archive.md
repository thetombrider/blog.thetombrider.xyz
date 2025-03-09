---
layout: page
title: Archivio
permalink: /archive/
---

{% assign date_format = site.date_format | default: "%b %-d, %Y" %}
{% for post in site.posts %}
  {% assign current_year = post.date | date: "%Y" %}
  {% if current_year != year %}
    {% unless forloop.first %}</ul>{% endunless %}
    <h2 id="y{{ current_year }}">{{ current_year }}</h2>
    <ul>
    {% assign year = current_year %}
  {% endif %}
  <li>
    <span>{{ post.date | date: date_format }}</span>
    <a href="{{ post.url | relative_url }}">{{ post.title | escape }}</a>
  </li>
  {% if forloop.last %}</ul>{% endif %}
{% endfor %}