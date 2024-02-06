---
title: Home
---

# Welcome to 130lab!

Hello and welcome to 130lab! This is a place where you can learn and explore various programming concepts and technologies.

# Blogs

{% for post in site.posts %}
- [{{ post.title }}]({{ post.url }}) ({{ post.date | date: "%Y %B %d" }})
{% endfor %}
