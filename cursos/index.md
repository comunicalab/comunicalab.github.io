---
layout: page
title: Cursos
---

Os cursos de Comunicação e Artes da Universidade São Judas Tadeu formam profissionais para as múltiplas linguagens da comunicação contemporânea.

{% for curso in site.data.cursos %}
<div class="lista-item">
  <h2 id="{{ curso.slug }}">{{ curso.nome }}</h2>
  <p class="conecta-linhafina">{{ curso.duracao }}</p>
  {% if curso.campi %}
  <p class="conecta-linhafina">Campi: {{ curso.campi | join: ", " }}</p>
  {% endif %}
  {% if curso.turno %}
  <p class="conecta-linhafina">Turnos: {{ curso.turno | join: ", " }}</p>
  {% endif %}
</div>
{% endfor %}
