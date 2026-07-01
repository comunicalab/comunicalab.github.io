---
layout: page
title: Professores
---

Corpo docente dos cursos de Comunicação e Artes da Universidade São Judas Tadeu.

{% assign professores_ordenados = site.professores | sort: "nome" %}

{% if professores_ordenados.size > 0 %}
<div>
  {% for prof in professores_ordenados %}
  <div class="professor-card">
    {% if prof.foto %}
    <img src="{{ prof.foto | relative_url }}" alt="Foto de {{ prof.nome }}" class="professor-foto">
    {% else %}
    <div class="professor-foto" style="background:var(--color-tag-bg);display:flex;align-items:center;justify-content:center;font-size:1.5rem;color:var(--color-accent);">&#9786;</div>
    {% endif %}
    <div class="professor-info">
      <h2><a href="{{ prof.url | relative_url }}">{{ prof.nome }}</a></h2>
      {% if prof.titulacao %}<p>{{ prof.titulacao }}</p>{% endif %}
      {% if prof.cursos %}
      <p class="tags-list">
        {% for curso_slug in prof.cursos %}
          {% assign curso = site.data.cursos | where: "slug", curso_slug | first %}
          {% if curso %}
          <span class="tag">{{ curso.nome }}</span>
          {% else %}
          <span class="tag">{{ curso_slug }}</span>
          {% endif %}
        {% endfor %}
      </p>
      {% endif %}
    </div>
  </div>
  {% endfor %}
</div>
{% else %}
<p>Em breve: lista de professores.</p>
{% endif %}
