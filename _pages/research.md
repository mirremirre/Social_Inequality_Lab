---
layout: page
title: Research
permalink: /research/
description: Active research projects at the Social Inequality Lab.
nav: true
nav_order: 3
horizontal: false
---
<!-- pages/research.md -->
{% assign category_order = "Trust and Inequality|Financial Inequality and Social Capital|Biomarkers of Inequality" | split: "|" %}

<div class="projects">
  {% for cat in category_order %}
    {% assign cat_projects = site.projects | where: "category", cat | sort: "importance" %}
    {% if cat_projects.size > 0 %}
      <h2 class="category-title">{{ cat }}</h2>
      <div class="row row-cols-1">
        {% for project in cat_projects %}
          {% include projects.liquid %}
        {% endfor %}
      </div>
    {% endif %}
  {% endfor %}
</div>
