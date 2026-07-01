---
layout: page
title: "Assuntos"
---

{% comment %}Agrega tags de todos os tipos de conteúdo sem plugin{% endcomment %}
{% assign all_docs = site.posts | concat: site.trabalhos | concat: site.projetos | concat: site.eventos %}

{% assign all_tags = "" | split: "" %}
{% for doc in all_docs %}
  {% for tag in doc.tags %}
    {% unless all_tags contains tag %}
      {% assign all_tags = all_tags | push: tag %}
    {% endunless %}
  {% endfor %}
{% endfor %}
{% assign all_tags = all_tags | sort %}

{% for tag in all_tags %}
<section class="tag-section" id="{{ tag | slugify }}">
  <h2><a href="{{ '/tags/' | relative_url }}{{ tag | slugify }}/">{{ tag }}</a></h2>
  <ul>
    {% for doc in all_docs %}
      {% if doc.tags contains tag %}
      <li>
        <a href="{{ doc.url | relative_url }}">{{ doc.title | default: doc.titulo }}</a>
        <span class="entry-date">{{ doc.date | default: doc.data | date: "%d/%m/%Y" }}</span>
      </li>
      {% endif %}
    {% endfor %}
  </ul>
</section>
{% endfor %}
