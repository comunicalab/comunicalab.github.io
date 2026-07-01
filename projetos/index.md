---
layout: page
title: Projetos
---

Projetos de extensão, pesquisa, agências experimentais e núcleos de produção dos cursos de Comunicação e Artes da São Judas.

{% assign tipos = site.projetos | map: "tipo" | uniq | sort %}

{% if tipos.size > 0 %}
{% for tipo in tipos %}
{% assign projetos_do_tipo = site.projetos | where: "tipo", tipo | sort: "ano_inicio" | reverse %}
{% if projetos_do_tipo.size > 0 %}
<h2 class="section-heading" id="{{ tipo | slugify }}">
  <span class="badge badge-{{ tipo }}">{{ tipo | replace: "-", " " }}</span>
</h2>
<ul class="entry-list">
  {% for p in projetos_do_tipo %}
  <li class="lista-item">
    {% if p.imagem %}
    <img src="{{ p.imagem | relative_url }}" alt="{{ p.titulo }}" style="max-height:180px;object-fit:cover;width:100%;">
    {% endif %}
    {% if p.ano_inicio %}<span class="entry-date">desde {{ p.ano_inicio }}</span>{% endif %}
    <h2><a href="{{ p.url | relative_url }}">{{ p.titulo }}</a></h2>
    {% if p.descricao %}<p>{{ p.descricao | truncate: 200 }}</p>{% endif %}
    {% if p.tags %}
    <p class="tags-list">
      {% for tag in p.tags %}
      <a href="{{ '/tags/' | relative_url }}{{ tag | slugify }}/" class="tag">{{ tag }}</a>
      {% endfor %}
    </p>
    {% endif %}
  </li>
  {% endfor %}
</ul>
{% endif %}
{% endfor %}

{% else %}
{% for p in site.projetos %}
<ul class="entry-list">
  <li class="lista-item">
    <h2><a href="{{ p.url | relative_url }}">{{ p.titulo }}</a></h2>
    {% if p.descricao %}<p>{{ p.descricao | truncate: 200 }}</p>{% endif %}
  </li>
</ul>
{% endfor %}
{% endif %}
