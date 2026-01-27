---
layout: default
title: Home
---

# Välkommen
Här är min site.

## Senaste inlägg
<ul>
  {% raw %}{% for post in site.posts limit:6 %}{% endraw %}
    <li>
      <a href="{% raw %}{{ post.url }}{% endraw %}">{% raw %}{{ post.title }}{% endraw %}</a>
      <small>({% raw %}{{ post.date | date: "%Y-%m-%d" }}{% endraw %})</small>
    </li>
  {% raw %}{% endfor %}{% endraw %}
</ul>
