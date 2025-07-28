---
title: Portal
layout: blog
---

### Interesting Stuff
<ul>
{% assign interesting_items = site.data.portal.interesting_stuff | sort: 'title' | where_exp: "item", "item.title" %}
{% for item in interesting_items %}
    <li><a href="{{ item.link }}" target="_blank" rel="noopener noreferrer">{{ item.title }}</a></li>
{% endfor %}
</ul>

### Academia
<ul>
{% assign interesting_items = site.data.portal.academia | sort: 'title' | where_exp: "item", "item.title" %}
{% for item in interesting_items %}
    <li><a href="{{ item.link }}" target="_blank" rel="noopener noreferrer">{{ item.title }}</a></li>
{% endfor %}
</ul>

### Tech Related
<ul>
{% assign interesting_items = site.data.portal.tech_related | sort: 'title' | where_exp: "item", "item.title" %}
{% for item in interesting_items %}
    <li><a href="{{ item.link }}" target="_blank" rel="noopener noreferrer">{{ item.title }}</a></li>
{% endfor %}
</ul>

### Language Learning Resources
**English**
<ul>
    {% assign LLR_items = site.data.portal.language_learning_resources["English"] | sort: 'title' | where_exp: "item", "item.title" %}
    {% for item in LLR_items %}
        <li><a href="{{ item.link }}" target="_blank" rel="noopener noreferrer">{{ item.title }}</a></li>
    {% endfor %}
</ul>

**Japanese**
<ul>
    {% assign LLR_items = site.data.portal.language_learning_resources["Japanese"] | sort: 'title' | where_exp: "item", "item.title" %}
    {% for item in LLR_items %}
        <li><a href="{{ item.link }}" target="_blank" rel="noopener noreferrer">{{ item.title }}</a></li>
    {% endfor %}
</ul>
