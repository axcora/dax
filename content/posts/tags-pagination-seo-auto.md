---
title: Tags, Pagination and SEO Auto - No Plugin Needed
description: DAX generates tags pages, pagination and sitemap.xml, rss.xml, robots.txt automatically without plugins
layout: minimal/post.dax
image: /img/blazorrazorkiller.webp
date: 2026-07-31
tags: [seo, tags, pagination, tutorial]
---


## Tags

Add in frontmatter:

```yaml
tags: [csharp, dax]
```

DAX auto generates:

- `/tags/` → list all tags (`all_tags`)
- `/tags/csharp/` → all posts with tag csharp using `tag.dax` layout

## Pagination

Controller file `content/posts.md`:

```yaml
---
title: Blog
layout: posts-list.dax
collection: posts
pagination: 6
---
```

Generates `/posts/`, `/posts/page/2/`, with variables:

- `pagination.items` (6 posts)
- `pagination.page`, `total_pages`
- `pagination.prev_url`, `next_url`

## SEO Auto

Every build generates:

- `sitemap.xml` from all pages + posts
- `robots.txt`
- `rss.xml` from `collections.posts`

No plugin, no config. Lighthouse 100 out of box.
