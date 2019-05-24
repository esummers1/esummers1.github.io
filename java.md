---
bg: "compass.jpg"
layout: page
title: "Java Lessons"
crawlertitle: "Java Lessons"
permalink: /java/
summary: ""
active: true
---

The project that sparked the creation of this blog was teaching Java programming to a colleague. Here are all the lessons, in order:

<ul class="year">
  {% for post in site.posts reversed %}
    {% if post.tags contains "java" %}
      <li>
          <a href="{{ post.url | relative_url}}">{{ post.title }}</a>
          <span class="date">{{ post.date | date: "%d-%m-%Y"  }}</span>
      </li>
    {% endif %}
  {% endfor %}
</ul>