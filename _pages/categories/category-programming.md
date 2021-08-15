---
layout: archive
title: "Posts by Programming"
permalink: /categories/Programming
author_profile: true
toc: true
---
{% for category in site.categories %}
  {% if category[0] == "Programming" %}
    {% for post in category[1] %}
      {% include archive-single.html type=list %}
    {% endfor %}
  {% endif %}  
{% endfor %}  
