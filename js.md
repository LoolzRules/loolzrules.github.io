---
layout: js
permalink: /js/
---
# Добро пожаловать!

## Архив моих поделок:

<ul>
    {%- for page in site.js -%}
        <li><a href="{{ page.url | remove: 'index.html' }}">{{ page.name | default: page.title }}</a></li>
    {%- endfor -%}
</ul>