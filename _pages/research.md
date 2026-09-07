---
layout: page
title: Research
permalink: /research/
description: Active research projects at the Social Inequality Lab.
nav: true
nav_order: 3
horizontal: false
---

{% assign category_order = "Trust and Inequality|Financial Inequality and Social Capital|Biomarkers of Inequality" | split: "|" %}

<div class="category-tabs">
  {% for cat in category_order %}
    <button class="category-tab" data-category="{{ cat | slugify }}">{{ cat }}</button>
  {% endfor %}
</div>

<div class="projects">
  {% for cat in category_order %}
    {% assign cat_projects = site.projects | where: "category", cat | sort: "importance" %}
    {% if cat_projects.size > 0 %}
      <div class="category-section" id="{{ cat | slugify }}" style="display: none;">
        <h2 class="category-title">{{ cat }}</h2>
        <div class="row row-cols-1">
          {% for project in cat_projects %}
            {% include projects.liquid %}
          {% endfor %}
        </div>
      </div>
    {% endif %}
  {% endfor %}
</div>

<script>
document.addEventListener('DOMContentLoaded', function () {
  const tabs = document.querySelectorAll('.category-tab');
  const sections = document.querySelectorAll('.category-section');

  tabs.forEach(tab => {
    tab.addEventListener('click', function () {
      const target = this.dataset.category;

      sections.forEach(section => {
        section.style.display = section.id === target ? 'block' : 'none';
      });

      tabs.forEach(t => t.classList.remove('active'));
      this.classList.add('active');
    });
  });

  // Show the first category by default
  if (tabs.length > 0) tabs[0].click();
});
</script>

<style>
.category-tabs {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
  flex-wrap: wrap;
}

.category-tab {
  padding: 8px 16px;
  border: 1px solid #ccc;
  border-radius: 20px;
  background: transparent;
  cursor: pointer;
  font-size: 0.95rem;
}

.category-tab.active {
  background: #333;
  color: #fff;
  border-color: #333;
}
</style>
