---
layout: page
title: Trabalhos
---

Arquivo de trabalhos acadêmicos produzidos nos cursos de Comunicação e Artes da São Judas. Cada entrada é um resultado de disciplina, organizado pelo projeto ao qual pertence.

{% assign projetos_ordenados = site.projetos | sort: "ano_inicio" | reverse %}

{% for projeto in projetos_ordenados %}
{% assign projeto_slug = projeto.path | remove: "_projetos/" | remove: ".md" %}
{% assign trabalhos_do_projeto = site.trabalhos | where: "projeto", projeto_slug | sort: "date" | reverse %}
{% if trabalhos_do_projeto.size > 0 %}
<h2 class="section-heading" id="projeto-{{ projeto_slug | slugify }}">
  <a href="{{ projeto.url | relative_url }}">{{ projeto.titulo }}</a>
</h2>
<ul class="entry-list">
  {% for t in trabalhos_do_projeto %}
  <li class="lista-item">
    {% if t.imagem %}
    <img src="{{ t.imagem | relative_url }}" alt="{{ t.title }}" style="max-height:180px;object-fit:cover;width:100%;">
    {% endif %}
    <span class="entry-date">{{ t.date | date: "%d/%m/%Y" }}</span>
    <h2><a href="{{ t.url | relative_url }}">{{ t.title }}</a></h2>
    <p class="conecta-linhafina">{{ t.uc }}</p>
    {% if t.descricao %}<p>{{ t.descricao | truncate: 180 }}</p>{% endif %}
    {% if t.tags %}
    <p class="tags-list">
      {% for tag in t.tags %}
      <a href="{{ '/tags/' | relative_url }}{{ tag | slugify }}/" class="tag">{{ tag }}</a>
      {% endfor %}
    </p>
    {% endif %}
  </li>
  {% endfor %}
</ul>
{% endif %}
{% endfor %}

{% assign trabalhos_sem_projeto = site.trabalhos | where_exp: "t", "t.projeto == nil" %}
{% if trabalhos_sem_projeto.size > 0 %}
<h2 class="section-heading" id="sem-projeto">Sem projeto vinculado</h2>
<ul class="entry-list">
  {% for t in trabalhos_sem_projeto %}
  <li class="lista-item">
    {% if t.imagem %}
    <img src="{{ t.imagem | relative_url }}" alt="{{ t.title }}" style="max-height:180px;object-fit:cover;width:100%;">
    {% endif %}
    <span class="entry-date">{{ t.date | date: "%d/%m/%Y" }}</span>
    <h2><a href="{{ t.url | relative_url }}">{{ t.title }}</a></h2>
    <p class="conecta-linhafina">{{ t.uc }}</p>
    {% if t.descricao %}<p>{{ t.descricao | truncate: 180 }}</p>{% endif %}
    {% if t.tags %}
    <p class="tags-list">
      {% for tag in t.tags %}
      <a href="{{ '/tags/' | relative_url }}{{ tag | slugify }}/" class="tag">{{ tag }}</a>
      {% endfor %}
    </p>
    {% endif %}
  </li>
  {% endfor %}
</ul>
{% endif %}
