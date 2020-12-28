---
layout: default
title: Collection
---
<h1>Collection</h1>

<ul>
  {% for collection in site.collection %}
    <li>
      <h2><a href="{{ author.url }}">{{ collection.name }}</a></h2>
      <h3>{{ collection.position }}</h3>
      <p>{{ collection.content | markdownify }}</p>
    </li>
  {% endfor %}
</ul>