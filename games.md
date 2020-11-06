---
layout: game
permalink: /games/
---
# Добро пожаловать!

## Архив игр:

<ul>
    {%- for game in site.games -%}
        <li><a href="{{ game.url | remove: 'index.html' }}">{{ game.name | default: game.title }}</a></li>
    {%- endfor -%}
</ul>