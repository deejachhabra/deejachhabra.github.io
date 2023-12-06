---
layout: default
title: "Get to know me!"
---

{% if site.show_excerpts %}
  {% include home.html %}
{% else %}
  {% include archive.html title="<strong style="font-family: monospace; color: #f45;">SELECT * FROM education WHERE person == 'DEEJA CHHABRA';</strong>" %}
{% endif %}
