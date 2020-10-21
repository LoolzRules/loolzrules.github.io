---
title: Главная
layout: post
permalink: /channel/
---

# Добро пожаловать!

__На репите каждый день__ - это телеграм-канал, посвящённый музыке.
Посты на канале выходят чуть больше чем раз в день, при этом каждый день посвящён одному исполнителю.
Здесь редко появляются музыкальные новинки, зато очень часто появляются песни, которые вы скорее всего не слышали.

## Список всех постов:

<ul>
{% for post in site.posts %}
    <li><a href="{{ post.url | remove: 'index.html' }}" class="draft">{{ post.name | default: post.title }}</a></li>
{% endfor %}
{% for post in site.channel %}
    <li>{{ post.date | date: "%Y.%m.%d" }} - <a href="{{ post.url | remove: 'index.html' }}">{{ post.name | default: post.title }}</a></li>
{% endfor %}
</ul>