---
layout: default
title: "Get to know me!"
---

{% if site.show_excerpts %}
  {% include home.html %}
{% else %}
  {% include archive.html %}
{% endif %}
