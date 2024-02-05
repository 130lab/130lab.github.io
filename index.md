---
title: Home
---

# Welcome to 130lab!

Hello and welcome to 130lab! This is a place where you can learn and explore various programming concepts and technologies.

## Getting Started

To get started, let's write a simple "Hello, World!" program in your favorite programming language.

# All Posts

{% for post in site.posts %}
- ({{ post.date | date: "%B %d, %Y" }}) [{{ post.title }}]({{ post.url }})
{% endfor %}

{% for post in site.posts %}
- [{{ post.title }}]({{ post.url }})
{% endfor %}

```python

print("Hello, World!")

```

[Check out our latest blogs](blogs/2022-01-01-Hellow-World.md)

