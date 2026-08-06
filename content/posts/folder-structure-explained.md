---
title: DAX Folder Structure Explained - Minimalist but Powerful
description: Complete guide to DAX folder structure - _data, content, templates, public, site
layout: minimal/post.dax
image: /img/dotnetssg.webp
date: 2026-07-30
tags: [docs, structure, beginner]
---


## Structure

```
│   Dax.csproj, Program.cs
├───_data/ → metadata.json, config.yaml, nav.json
├───content/ → index.md → /, about.md → /about/, posts.md + posts/hello.md → /posts/hello/
├───templates/layouts/ → base.dax, home.dax, posts-list.dax, post.dax, tag.dax
├───templates/partials/ → header.dax, footer.dax, seo.dax
├───public/ → css/, img/ → copied to site/
└───site/ → output (gitignored)
```

### Why this?

- `_data/` = global data, accessible `{{ config.nav }}`, `{{ metadata.title }}`
- `content/` = markdown files, URL = file path
- `templates/` = layouts + partials, `{% include header.dax %}`
- `public/` = static assets copied verbatim
- `site/` = build output, never edit

`.gitignore` must include `bin/`, `obj/`, `site/`.
