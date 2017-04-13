---
layout: page
title: "Содержание"
date: 2017-03-24
permalink: contents.html
description: |
  Полное содержание блога, список всех статей
  опубликованных, начиная с марта 2017-го года.
---

<!-- Всего: {{ site.posts.size }}. -->

{% for post in site.posts %}
  <div style="margin-bottom:1.2em">
    <a href="{{ post.url }}" class="title" style="font-size:1.4em">
      <span itemprop="name headline mainEntityOfPage">{{ post.title }}</span>
    </a>
    <br/>
    <ul class="inline subline">
      <li>
        {{ post.author }}
      </li>
      <li>
        <time itemprop="datePublished dateModified" datetime="{{ post.date | date_to_xmlschema }}">
          {% assign m = post.date | date: "%-m" %}
          {{ post.date | date: "%-d" }}
          {% case m %}
            {% when '1' %}января
            {% when '2' %}февраля
            {% when '3' %}марта
            {% when '4' %}апреля
            {% when '5' %}мая
            {% when '6' %}июня
            {% when '7' %}июля
            {% when '8' %}августа
            {% when '9' %}сентября
            {% when '10' %}октября
            {% when '11' %}ноября
            {% when '12' %}декабря
          {% endcase %}
          {{ post.date | date: "%Y" }}
        </time>
      </li>
      <!--
      <li>
        <a href="{{ site.url }}{{ post.url }}#disqus_thread" itemprop="discussionUrl">комментарии</a>
      </li>
      -->
    </ul>
  </div>
{% endfor %}

