---
layout: page
title: Eventos
---

Eventos acadêmicos, semanas temáticas, ciclos de estudos e atividades de extensão dos cursos de Comunicação e Artes da São Judas.

{% assign eventos_ordenados = site.eventos | sort: "data" | reverse %}

{% if eventos_ordenados.size > 0 %}
<ul class="entry-list">
  {% for e in eventos_ordenados %}
  <li class="lista-item">
    {% if e.imagem %}
    <img src="{{ e.imagem | relative_url }}" alt="{{ e.titulo }}" style="max-height:180px;object-fit:cover;width:100%;">
    {% endif %}
    <p style="margin:0.4rem 0;">
      <span class="entry-date">{{ e.data | date: "%d/%m/%Y" }}{% if e.data_fim %} a {{ e.data_fim | date: "%d/%m/%Y" }}{% endif %}</span>
      {% if e.categoria %}&nbsp;<span class="badge badge-{{ e.categoria }}">{{ e.categoria | replace: "-", " " }}</span>{% endif %}
    </p>
    <h2><a href="{{ e.url | relative_url }}">{{ e.titulo }}</a></h2>
    {% if e.local %}<p class="conecta-linhafina">{{ e.local }}</p>{% endif %}
    {% if e.descricao %}<p>{{ e.descricao | truncate: 200 }}</p>{% endif %}
    {% if e.tags %}
    <p class="tags-list">
      {% for tag in e.tags %}
      <a href="{{ '/tags/' | relative_url }}{{ tag | slugify }}/" class="tag">{{ tag }}</a>
      {% endfor %}
    </p>
    {% endif %}
  </li>
  {% endfor %}
</ul>
{% else %}
<p>Em breve: programação de eventos.</p>
{% endif %}
