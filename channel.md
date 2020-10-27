---
layout: post
permalink: /channel/
months: [Январь, Февраль, Март, Апрель, Май, Июнь, Июль, Август, Сентябрь, Октябрь, Ноябрь, Декабрь]
---
# Добро пожаловать!

__На репите каждый день__ - это блог, посвящённый музыке. Посты выходят чуть больше чем раз в день,
при этом каждый день посвящён одному исполнителю. Здесь редко появляются музыкальные новинки,
зато часто появляются песни, которые вы, скорее всего, не слышали.

## Архив:

{% assign num_of_posts = site.posts | size -%}
{%- unless num_of_posts == 0 -%}
<div class="accordion">
    <input type="checkbox" id="drafts" checked="true"/>
    <label for="drafts"><h4>Черновики</h4></label>
    <div class="content">
        <ul>
            {%- for post in site.posts -%}
                <li><a href="{{ post.url | remove: 'index.html' }}" class="draft">{{ post.name | default: post.title }}</a></li>
            {%- endfor -%}
        </ul>
    </div>
</div>
{%- endunless -%}

{%- assign postsByYear =  site.channel | group_by_exp: "post", "post.date | date: '%Y'" -%}
{%- for year in postsByYear -%}
    <h3 class="year">{{ year.name }}</h3>
    {%- assign postsByMonth =  year.items | group_by_exp: "post", "post.date | date: '%m'" -%}
    {%- for month in postsByMonth -%}
        {%- assign month_index = month.name | minus: 1 -%}
        {%- assign accordion_id = year.name | append: "_" | append: month_index -%}
        <div class="accordion">
            <input type="checkbox" id="{{ accordion_id }}"/>
            <label for="{{ accordion_id }}"><h4>{{ page.months[month_index] }}</h4></label>
            <div class="content">
                <ul>
                    {%- for post in month.items -%}
                        <li><a href="{{ post.url }}">{{ post.name | default: post.title }}</a></li>
                    {%- endfor -%}
                </ul>
            </div>
        </div>
    {%- endfor -%}
{%- endfor -%}

<script type="application/javascript">
    const inputs = document.querySelectorAll('.accordion > input');
    const now = new Date();
    const date_now_id = `${now.getFullYear()}_${now.getMonth()}`;
    for (const i of inputs)
        if (i.id === date_now_id)
            i.checked = true;
</script>