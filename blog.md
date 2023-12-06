---
layout: default
title: "Get to know me!"
---
<strong style="font-family: monospace; color: #f45;">SELECT * FROM projects WHERE person == 'DEEJA CHHABRA';</strong>
{% if site.show_excerpts %}
  {% include home.html %}
{% else %}
  {% include archive.html title="Posts" %}
{% endif %}
