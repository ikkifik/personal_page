---
title: Blog
layout: blog
---

<!-- Group by post categories -->
{% assign postsByCategories = site.posts | sort: 'category' | group_by_exp: "post", "post.category"   %}
{% for category in postsByCategories %}
  <h3 id="{{ category.name }}"><a href="#{{ category.name }}">#</a> {{ category.name | replace: "-", " "}}</h3>
  <ul>
    {% assign itemsSortedByDate = category.items | sort: 'date' %}
    {% assign itemsSortedByTitle = itemsSortedByDate | sort: 'title' %}
    {% for post in itemsSortedByTitle %}
      <li><a href="{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %} 
  </ul>
{% endfor %}