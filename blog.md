---
layout: default
---
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>{{ page.title }}</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 20px;
    }

    .sql-query {
      font-family: monospace;
      color: #f45;
      font-weight: bold;
      margin-top: 50px;
      margin-left: 140px;
      margin-bottom: 20px; /* Adjust the margin as needed */
    }
  </style>
</head>
<body>

<div class="sql-query">
  <b>SELECT * FROM blogs WHERE person == "DEEJA CHHABRA";</b>
</div>

{% if site.show_excerpts %}
  {% include home.html %}
{% else %}
  {% include archive.html %}
{% endif %}
