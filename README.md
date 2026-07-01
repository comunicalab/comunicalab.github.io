# Guia de Publicação e Manutenção — ComunicaLab

Este é o site experimental para o ComunicaLab da São Judas: comunicalab.github.io.

O guia cobre as operações mais comuns: publicar professores, projetos, eventos, trabalhos e notícias, além de manter cursos, tags e o site no ar.

---

## Como o site funciona

O site usa [Jekyll](https://jekyllrb.com/) publicado via GitHub Pages. Cada conteúdo é um arquivo de texto em Markdown (`.md`) com um cabeçalho de metadados (*front matter*) entre `---`. O Jekyll converte esses arquivos em HTML automaticamente a cada `push` para o repositório.

Não há painel de administração. Para publicar, você edita ou cria um arquivo de texto e envia para o GitHub por meio do seu perfil. Converse com a coordenação do ComunicaLab para saber mais.

---

## Visão geral da arquitetura

O conteúdo é organizado em **coleções**, e elas se referenciam entre si por *slug* (o nome do arquivo, sem extensão):

```
_professores/   → pessoas do corpo docente
_projetos/      → projetos de extensão, pesquisa, agências, núcleos
_eventos/       → eventos, semanas temáticas, ciclos
_trabalhos/     → trabalhos de disciplina/mostra, ligados a um projeto e a professores
_posts/         → notícias do blog
_data/cursos.yml → lista de cursos (não é coleção, é dado fixo)
```

**Como as referências funcionam:**

- Um **trabalho** pode apontar para um `projeto` (campo `projeto: a-mooca-ta-on`, o slug do arquivo em `_projetos/`) e para um ou mais `professores` (slugs de `_professores/`).
- Um **projeto** também lista `professores` responsáveis pelo mesmo mecanismo.
- Um **professor** lista `cursos` pelos `slug`s definidos em `_data/cursos.yml`.
- As páginas de listagem (`/professores/`, `/projetos/`) e os próprios layouts cruzam essas referências automaticamente — por exemplo, a página de um professor mostra sozinha os trabalhos e projetos em que ele aparece. **Não é preciso editar nada manualmente em mais de um lugar.**

> Sempre use o slug exato do arquivo (nome do arquivo sem `.md`) ao referenciar professores e projetos. Se o slug não bater com nenhum arquivo, o site exibe o texto digitado como fallback, mas sem link.

---

## 1. Professor

Crie um arquivo em `_professores/slug-do-nome.md`:

```
_professores/maria-fernandes.md
```

```markdown
---
nome: Maria Fernandes
titulacao: Doutora em Comunicação
cursos: [jornalismo, publicidade]
coordenacao: false
email: maria.fernandes@usjt.edu.br
lattes: "http://lattes.cnpq.br/0000000000000000"
foto: "/assets/img/professores/maria-fernandes.webp"
---

Texto livre opcional sobre a trajetória do professor (aparece abaixo dos dados).
```

| Campo | Obrigatório | Descrição |
|-------|-------------|-----------|
| `nome` | sim | Nome de exibição |
| `titulacao` | recomendado | Ex.: "Mestre em Comunicação" |
| `cursos` | recomendado | Lista de `slug`s definidos em `_data/cursos.yml` |
| `coordenacao` | opcional | `true`/`false` |
| `email` | opcional | Vira link `mailto:` |
| `lattes` | opcional | URL do Currículo Lattes |
| `linkedin` | opcional | URL do LinkedIn |
| `portfolio` | opcional | URL do portfólio |
| `foto` | opcional | Caminho da foto; sem ela, mostra um ícone padrão |

Os trabalhos e projetos do professor aparecem automaticamente na página dele.

---

## 2. Projeto

Crie um arquivo em `_projetos/slug-do-projeto.md`:

```
_projetos/agencia-experimental.md
```

```markdown
---
titulo: "Agência Experimental"
tipo: agencia
descricao: "Agência-escola que atende clientes reais sob orientação docente."
professores: [andre-rosa]
ano_inicio: 2024
link: ""
imagem: "/assets/img/projetos/agencia-experimental.webp"
tags: [agencia, publicidade, pratica-profissional]
---

Texto livre opcional com mais detalhes sobre o projeto.
```

| Campo | Obrigatório | Descrição |
|-------|-------------|-----------|
| `titulo` | sim | Título do projeto |
| `tipo` | sim | Categoria livre (ex.: `extensao`, `pesquisa`, `agencia`, `nucleo`) — vira selo (badge) e agrupa a listagem em `/projetos/` |
| `descricao` | sim | Resumo curto |
| `professores` | sim | Lista de slugs de `_professores/` |
| `ano_inicio` | recomendado | Ano de início do projeto |
| `link` | opcional | URL externa do projeto |
| `imagem` | opcional | Imagem de capa |
| `tags` | recomendado | Palavras-chave (veja seção Tags) |

Os trabalhos vinculados a este projeto (campo `projeto:` no trabalho) aparecem automaticamente na página dele.

---

## 3. Evento

Crie um arquivo em `_eventos/slug-do-evento.md`:

```
_eventos/semana-comunicacao-2026.md
```

```markdown
---
titulo: "Semana de Comunicação e Artes 2026"
data: 2026-05-11
data_fim: 2026-05-15
categoria: eventos
local: "Auditório Principal — Campus Mooca"
descricao: "Semana temática anual com palestras, workshops e mostras de trabalhos."
tags: [semana, comunicacao, artes]
link: ""
imagem: "/assets/img/eventos/semana-2026.webp"
---

Texto livre opcional com programação detalhada.
```

| Campo | Obrigatório | Descrição |
|-------|-------------|-----------|
| `titulo` | sim | Título do evento |
| `data` | sim | Data de início, formato `AAAA-MM-DD` |
| `data_fim` | opcional | Data de encerramento, se o evento durar mais de um dia |
| `categoria` | recomendado | Ex.: `eventos`, `palestra`, `oficina` — vira selo e aparece na listagem |
| `local` | recomendado | Onde acontece |
| `descricao` | sim | Resumo curto |
| `link` | opcional | URL externa com mais informações |
| `imagem` | opcional | Imagem de capa |
| `tags` | recomendado | Palavras-chave |

---

## 4. Trabalho

Crie um arquivo em `_trabalhos/` seguindo a convenção de nome:

```
_trabalhos/projeto-slug-do-titulo.md
```

Exemplo: `_trabalhos/mostra-2026-1-identidade-mooca.md`

```markdown
---
layout: trabalho
title: "Título do Trabalho"
uc: "Nome da Unidade Curricular"
professores:
  - andre-rosa
alunos:
  - "Nome do Aluno"
  - "Outro Aluno"
descricao: "Uma ou duas frases descrevendo o trabalho."
link: "https://link-para-o-trabalho.com"
imagem: "/assets/img/trabalhos/nome-descritivo.webp"
projeto: a-mooca-ta-on
tags: [tag1, tag2, mostra-2026-1]
date: 2026-06-27
---
```

| Campo | Obrigatório | Descrição |
|-------|-------------|-----------|
| `title` | sim | Título do trabalho |
| `uc` | sim | Unidade curricular (disciplina) |
| `professores` | sim | Lista de **slugs** de `_professores/` (não o nome — ex.: `andre-rosa`, não "André Rosa") |
| `alunos` | sim | Lista de nomes dos alunos (texto livre, sem coleção própria) |
| `descricao` | sim | Resumo curto (aparece nas listagens) |
| `link` | recomendado | URL do trabalho publicado |
| `imagem` | opcional | Caminho da imagem: `/assets/img/trabalhos/nome.webp` |
| `projeto` | sim | Slug de um arquivo em `_projetos/` — é esse vínculo que agrupa o trabalho na página `/trabalhos/` |
| `tags` | recomendado | Palavras-chave (veja seção Tags) |
| `date` | sim | Data no formato `AAAA-MM-DD` |

> A página `/trabalhos/` agrupa automaticamente os trabalhos pelo `projeto` a que pertencem (ex.: "A Mooca Tá On", "Mostra de Trabalhos 2026.1"), na ordem de `ano_inicio` dos projetos. Uma mostra semestral (ex.: "Mostra de Trabalhos 2026.1") é, ela própria, um projeto em `_projetos/` — veja a seção [Adicionar uma nova Mostra](#adicionar-uma-nova-mostra-novo-semestre) em Manutenção.

---

## 5. Notícia

Crie um arquivo em `_posts/` com o nome obrigatoriamente no formato:

```
_posts/AAAA-MM-DD-slug-do-titulo.md
```

Exemplo: `_posts/2026-08-15-workshop-podcast.md`

```markdown
---
layout: post
title: "Título da Notícia"
date: 2026-08-15
tags: [podcast, oficina, comunicacao]
---

Texto da notícia em Markdown. Parágrafos separados por linha em branco.

Pode usar **negrito**, *itálico* e [links](https://exemplo.com).
```

---

## 6. Cursos

Os cursos **não são uma coleção** (não há um arquivo por curso). Eles ficam todos juntos em `_data/cursos.yml` e são listados na página `/cursos/`. Professores referenciam cursos por `slug` no campo `cursos:` do front matter.

```yaml
- slug: jornalismo
  nome: Jornalismo
  duracao: "4 anos / 8 semestres"
  campi: [Mooca, Butantã]
  turno: [manhã, noite]
```

Para adicionar um curso novo, acrescente um bloco como esse ao final de `_data/cursos.yml`, usando um `slug` único em letras minúsculas e hífens.

---

## 7. Tags

Tags são palavras-chave que agrupam conteúdos relacionados. Existem dois lugares onde elas aparecem:

- **`/tags/`** — índice geral, gerado automaticamente. Ele varre `posts`, `trabalhos`, `projetos` e `eventos` via Liquid e monta a lista completa de tags em uso, sem precisar de cadastro manual.
- **`/tags/<nome-da-tag>/`** — página dedicada de cada tag (ex.: `/tags/mooca/`), com URL própria para divulgar/linkar. Essas páginas **não são geradas automaticamente** — o GitHub Pages roda o build legado do Jekyll, que não permite plugins de geração de páginas (tipo `jekyll-archives`). Por isso cada tag precisa de um arquivo pré-criado.

> Páginas de **professores** não entram no índice de tags — elas não têm campo `tags`.

### Página de uma tag nova

Sempre que usar uma tag que ainda não tem página dedicada, crie o arquivo:

```
tags/nome-da-tag/index.md
```

Exemplo, para a tag `podcast`:

```markdown
---
layout: tag
title: "Podcast"
tag: podcast
---
```

| Campo | Descrição |
|-------|-----------|
| `layout` | sempre `tag` |
| `title` | nome de exibição da tag (pode ter acento e maiúscula) |
| `tag` | o valor **exatamente igual** ao usado no campo `tags:` dos outros arquivos (minúsculo, com hífen) |

O layout `tag.html` já filtra sozinho todo o conteúdo (`posts`, `trabalhos`, `projetos`, `eventos`) que contém essa tag — não precisa listar nada manualmente. Se esquecer de criar a página, o link gerado em `/tags/` ou no rodapé de um item aponta para uma URL que ainda não existe (404) — é o sinal de que falta criar o arquivo.

**Boas práticas:**

- Use letras minúsculas e hífens: `comunicacao-urbana`, não `Comunicação Urbana`
- Seja consistente: se já existe `mooca`, não crie `a-mooca`
- Inclua sempre a tag da mostra nos trabalhos: `mostra-2026-1`
- Máximo de 5 a 7 tags por item

---

## 8. Imagens

- Formato preferido: **WebP** (menor tamanho, boa qualidade)
- Resolução recomendada: 1200 × 675 px (proporção 16:9)
- Salve por tipo de conteúdo, para manter organizado:
  - `assets/img/trabalhos/nome-descritivo.webp`
  - `assets/img/projetos/nome-descritivo.webp`
  - `assets/img/eventos/nome-descritivo.webp`
  - `assets/img/professores/nome-descritivo.webp`
- Referencie no front matter correspondente: `imagem: "/assets/img/trabalhos/nome-descritivo.webp"` (professores usam o campo `foto`)

Para converter imagens para WebP no Windows, use o [Squoosh](https://squoosh.app/) (gratuito, roda no navegador).

---

## 9. Pré-visualização local

Requer Ruby e Bundler instalados. Na pasta do projeto:

```bash
bundle install        # só na primeira vez
bundle exec jekyll serve
```

Acesse `http://localhost:4000` no navegador. O site atualiza automaticamente ao salvar arquivos.

---

## 10. Publicar no GitHub

Após criar ou editar arquivos:

```bash
cd /path/do/meu-site
git init
git config user.name "seu usuario"
git add .
git commit -m "Descrição da atualização"
git remote add origin url-do-repositorio
git push -u origin master:main
```

O GitHub Pages faz o build automaticamente. Em 1 a 2 minutos o site em `https://comunicalab.github.io` estará atualizado.

Se o build falhar, verifique em **Settings → Pages → Actions** do repositório para ver o erro.

---

## 11. Manutenção

### Atualizar o menu de navegação

Edite `_includes/header.html` e adicione um item à lista `.nav-menu`:

```html
<li{% if page.url contains "/novo-item" %} class="current-menu-item"{% endif %}>
  <a href="{{ '/novo-item/' | relative_url }}">Novo Item</a>
</li>
```

### Texto da home e do Sobre

- Home: edite `index.md` — o texto abaixo do `---` final é o parágrafo institucional exibido na página inicial.

- Sobre: edite `index.md` — os textos de cada bloco estão separados por intertítulos.


### Logotipos

O site usa dois logotipos em locais diferentes:

- **Cabeçalho** (ícone do Comunica-Lab, ao lado do nome do site): `assets/img/comunicalab-icon.png`, referenciado em `_includes/header.html`.
- **Rodapé** (selo da Universidade São Judas Tadeu): `assets/img/logo-usjt.svg`, referenciado em `_includes/footer.html`.

Para trocar, substitua o arquivo de imagem mantendo o nome (ou ajuste o caminho `src` no include correspondente):

```html
<!-- _includes/header.html -->
<img src="{{ '/assets/img/comunicalab-icon.png' | relative_url }}" alt="" aria-hidden="true">

<!-- _includes/footer.html -->
<img class="footer-usjt" src="{{ '/assets/img/logo-usjt.svg' | relative_url }}" alt="Universidade São Judas Tadeu">
```

---

## Referências rápidas

- Markdown: <https://www.markdownguide.org/basic-syntax/>
- Jekyll: <https://jekyllrb.com/docs/>
- GitHub Pages: <https://docs.github.com/pt/pages>
