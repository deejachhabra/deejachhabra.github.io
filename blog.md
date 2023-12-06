---
layout: default
---
<strong style="font-family: monospace; color: #f45;">SELECT * FROM passion WHERE person == "DEEJA CHHABRA";</strong> 
{% if site.show_excerpts %}
  {% include home.html %}
{% else %}
  {% include archive.html %}
{% endif %}
