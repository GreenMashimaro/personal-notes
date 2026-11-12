---
layout: default
title: 文档列表
---

## 文档列表

{% assign entries = site.pages | concat: site.static_files | sort: 'name' | reverse %}
{% capture links %}
  {% for entry in entries %}
    {% assign path = entry.path | prepend: '/' | replace_first: '//', '/' %}
    {% assign folder = path | slice: 0, 7 %}
    {% if folder != '/notes/' %}{% continue %}{% endif %}

    {% assign filename = entry.name %}
    {% assign year_separator = filename | slice: 4, 1 %}
    {% assign month_separator = filename | slice: 7, 1 %}
    {% assign title_separator = filename | slice: 10, 1 %}
    {% if year_separator != '-' or month_separator != '-' or title_separator != ' ' %}{% continue %}{% endif %}

    {% assign markdown_suffix = filename | slice: -3, 3 %}
    {% assign html_suffix = filename | slice: -5, 5 %}
    {% if markdown_suffix == '.md' and entry.url %}
      {% assign extension_length = 3 %}
      {% assign url = entry.url %}
    {% elsif html_suffix == '.html' %}
      {% assign extension_length = 5 %}
      {% assign url = entry.url | default: path %}
    {% else %}
      {% continue %}
    {% endif %}

    {% assign label_length = filename.size | minus: extension_length %}
    {% assign label = filename | slice: 0, label_length %}
    <li><a href="{{ url | relative_url | escape }}">{{ label | escape }}</a></li>
  {% endfor %}
{% endcapture %}
{% assign links = links | strip %}
{% if links != '' %}
<ul>
{{ links }}
</ul>
{% else %}
<p>还没有文档。</p>
{% endif %}
