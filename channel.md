---
layout: post
permalink: /channel/
months: [Январь, Февраль, Март, Апрель, Май, Июнь, Июль, Август, Сентябрь, Октябрь, Ноябрь, Декабрь]
---
# Добро пожаловать!

__На репите каждый день__ - это блог, посвящённый музыке. Посты выходят чуть чаще чем раз в день,
при этом каждый день посвящён одному исполнителю. Здесь редко появляются музыкальные новинки,
зато часто появляются песни, которые вы, скорее всего, не слышали.

## Архив:
{% assign num_of_posts = site.posts | size -%}
{%- unless num_of_posts == 0 -%}
<details class="accordion">
    <summary>Черновики</summary>
    <div class="content">
        <ul>
            {%- for post in site.posts -%}
                <li><a href="{{ post.url | remove: 'index.html' }}" class="draft">{{ post.name | default: post.title }}</a></li>
            {%- endfor -%}
        </ul>
    </div>
</details>
{%- endunless -%}

{%- assign nowunix = "now" | date: "%s" | plus: 0 -%}

{%- assign postsByYear = site.channel | reverse | group_by_exp: "post", "post.date | date: '%Y'" -%}
{%- for year in postsByYear -%}
    <h3 class="year">{{ year.name }}</h3>
    {%- assign postsByMonth =  year.items | group_by_exp: "post", "post.date | date: '%m'" -%}
    {%- for month in postsByMonth -%}
        {%- assign month_index = month.name | minus: 1 -%}
        {%- assign accordion_id = year.name | append: "_" | append: month_index -%}
        <details class="accordion" id="{{ accordion_id }}">
            <summary>{{ page.months[month_index] }}</summary>
            {%- assign month_items = month.items | reverse -%}
            <div class="content">
                <ul>
                    {%- for post in month_items -%}
                        {%- assign posttime = post.date | date: "%s" | plus: 0 -%}
                        {%- if site.future or posttime < nowunix -%}
                            <li><a href="{{ post.url }}">{{ post.name | default: post.title }}</a></li>
                        {%- endif -%}
                    {%- endfor -%}
                </ul>
            </div>
        </details>
    {%- endfor -%}
{%- endfor -%}

<script type="application/javascript">
    const accordions = document.querySelectorAll('.accordion');
    const now = new Date();
    const date_now_id = `${now.getFullYear()}_${now.getMonth()}`;
    for (const a of accordions)
        a.open = a.id === date_now_id;
</script>