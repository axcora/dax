---
title: Auto Collections and Free Nested Frontmatter - Jekyll Style but Faster
description: How DAX auto collections and unlimited nested YAML frontmatter works without fixed schema
image: /img/razorkiller.webp
layout: minimal/post.dax
date: 2026-08-01
tags: [tutorial, collections, frontmatter, jekyll]
---


## Auto Collections

Create folder `content/services/` and put `jas.md`, `desain.md` inside.

DAX auto generates `collections.services` sorted by date desc.

In template:

```dax
{% for item in collections.services %}
  <a href="{{ item.url }}">{{ item.title }}</a>
{% endfor %}
```

No config file needed.

## Free Nested Frontmatter

Unlike Blazor or fixed schema SSG, DAX frontmatter is **free**:

```yaml
hero:
  title: Welcome
  list:
    - name: GitHub
      url: https://github.com
      meta:
        icon: github
        deep:
          level: 3
```

Access in template:

```dax
{{ hero.title }}
{% for item in hero.list %}
  {{ item.name }} - {{ item.meta.deep.level }}
{% endfor %}
```

Unlimited depth. No struct definition. This is impossible in CAX.
