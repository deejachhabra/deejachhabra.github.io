---
layout: default
title: "Get to know me!"
---

{% if site.show_excerpts %}
  {% include home.html %}
{% else %}
  {% include archive.html title: "<b style=\"color: #f45;\">SELECT * FROM education WHERE person == 'DEEJA CHHABRA';"</b> %}
{% endif %}
