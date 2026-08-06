---
layout: minimal/page.dax
title: DAX Documentation
description: Complete guide for DAX - Pure C# Static Site Generator. Zero dependency, blazing fast, bento-ready.
image: /img/dotnetstaticsite.webp
---

# DAX - Dotnet by AXcora

**The fastest static starter. Clean bento grid, pure HTML + Axcora CSS. No build step required.**

DAX is a pure C# Static Site Generator (SSG) inspired by Eleventy (11ty), Jekyll, and Astro. Zero Node.js, zero webpack, build hundreds of pages in milliseconds.

- **Repo:** https://dax.axcora.com
- **Version:** 1.0.0
- **License:** Open Source Forever

## Quick Start

### Use dotnet slim version

```bash
git clone https://github.com/mesinkasir/dax
cd dax
dotnet run -- build
dotnet run -- start
open http://localhost:8080/
```

### Use dax version

```bash
git clone https://github.com/mesinkasir/dax
cd dax
dotnet publish -c Release -o .
dax build
dax start
open http://localhost:8080/
```

## Folder Structure

```
/
├── _data/              # Global data (JSON/YAML)
│   ├── metadata.json
│   ├── config.yaml
│   └── nav.json
├── content/            # Markdown content
│   ├── index.md
│   ├── posts.md        # Collection controller
│   ├── tags.md
│   └── posts/
│       ├── hello.md
│       └── ...
├── templates/
│   ├── layouts/        # Layouts (base, home, post, etc)
│   │   ├── base.dax
│   │   ├── minimal/
│   │   │   ├── page.dax
│   │   │   ├── post.dax
│   │   │   └── blog.dax
│   └── partials/       # Partials (header, footer, seo)
│       ├── header.dax
│       ├── footer.dax
│       └── minimal/
│           ├── bento1.dax
│           ├── bento2.dax
│           └── bento3.dax
├── public/             # Static assets (copied to site/)
│   ├── css/
│   ├── img/logo/
│   └── img/icon/
└── site/               # Generated output
```

## Frontmatter

Every `.md` file supports YAML frontmatter:

```yaml
---
layout: minimal/page.dax
title: My Page
description: SEO description
image: /img/og.jpg
date: 2026-08-06
tags: [csharp, dax, ssg]
---
```

Supported keys:
- `layout` - Layout file in `templates/layouts/`
- `title`, `description`, `image` - SEO
- `date` - For sorting collections
- `tags` - Array or string `[a, b]` or `a, b`
- `collection` - Mark file as collection controller
- `pagination` - Items per page (e.g. `6`)

## Layouts vs Partials

**IMPORTANT - They are separated!**

```csharp
// Layout - used via frontmatter
layout: minimal/blog.dax
-> loads from templates/layouts/minimal/blog.dax
// Partial - used via include
{ % include minimal/bento1.dax % }
-> loads from templates/partials/minimal/bento1.dax
```

Even if names are same (`minimal/blog.dax`), they never collide.

## Templating Engine

DAX uses Liquid-like syntax:

### Variables

```dax
{ { title } }
{ { metadata.title } }
{ { config.site_name } }
{ { page.url } }
{ { content } }
```

Fallback:

```dax
{ { image or metadata.image } }
```

### Includes

```dax
{ % include header.dax % }
{ % include minimal/bento1.dax % }
```

### If / Else

```dax
{ % if title % }
<h1>{ { title } }</h1>
{ % endif % }
{ % if pagination.has_prev % }
<a href="{ { pagination.prev_url } }">Prev</a>
{ % endif % }
{ % if prev_post % }
<a href="{ { prev_post.url } }">{ { prev_post.title } }</a>
{ % endif % }
```

Supports nested if:

```dax
{ % if prev_post % }
  { % if prev_post.image % }
    <img src="{ { prev_post.image } }" />
  { % endif % }
  <h3>{ { prev_post.title } }</h3>
{ % endif % }
```

Operators: `==`, `!=`, `or`, `and`, `||`, `&&`

### For Loop

```dax
{ % for post in collections.posts % }
<a href="{ { post.url } }">{ { post.title } }</a>
{ % endfor % }
{ % for post in collections.posts limit:3 % }
{ % for t in all_tags % }
{ { t.name } } ({ { t.count } })
{ % endfor % }
```

## Collections

Any folder inside `content/` becomes a collection.

`content/posts/my-post.md` -> collection `posts`

Create controller `content/posts.md`:

```yaml
---
layout: posts-list.dax
title: Blog
collection: posts
pagination: 6
---
```

Access in template:

```dax
{ { collections.posts } }
{ { pagination.items } }
{ { pagination.current_page } }
{ { pagination.total_pages } }
{ { pagination.has_prev } }
{ { pagination.has_next } }
{ { pagination.prev_url } }
{ { pagination.next_url } }
```

### Pagination Template (Safe)

```dax
{ % for post in pagination.items % }
<div><a href="{ { post.url } }">{ { post.title } }</a></div>
{ % endfor % }
<div>
{ % if pagination.has_prev % }<a href="{ { pagination.prev_url } }">Prev</a>{ % endif % }
Page { { pagination.current_page } }/{ { pagination.total_pages } }
{ % if pagination.has_next % }<a href="{ { pagination.next_url } }">Next</a>{ % endif % }
</div>
```

## Prev / Next Post

In `post.dax` layout:

```dax
{ % if has_prev % }
<a href="{ { prev_post.url } }">Prev { { prev_post.title } }</a>
{ % endif % }
{ % if has_next % }
<a href="{ { next_post.url } }">{ { next_post.title } } Next</a>
{ % endif % }
```

Or full card:

```dax
<div class="row">
<div class="col-6">
{ % if prev_post % }
<a href="{ { prev_post.url } }">
{ % if prev_post.image % }<img src="{ { prev_post.image or metadata.image } }" />{ % endif % }
<h3>{ { prev_post.title } }</h3>
</a>
{ % endif % }
</div>
<div class="col-6">
{ % if next_post % }
<a href="{ { next_post.url } }">
{ % if next_post.image % }<img src="{ { next_post.image or metadata.image } }" />{ % endif % }
<h3>{ { next_post.title } }</h3>
</a>
{ % endif % }
</div>
</div>
```

## Tags

Add tags in frontmatter:

```yaml
tags: [csharp, dax, tutorial]
```

Templates:

```dax
{ % for tag in tags % }{ { tag } }{ % endfor % }
{ % for t in all_tags % }
<a href="{ { t.url } }">{ { t.name } } ({ { t.count } })</a>
{ % endfor % }
```

Auto generates:
- `/tags/` - All tags list
- `/tags/{slug}/` - Tag pages

## Global Data

Files in `_data/` are auto-loaded:

`_data/config.yaml`:
```yaml
site_name: DAX
pagination_default: 6
list:
  - title: Blog
    url: /blog/
```

Use:

```dax
{ { config.site_name } }
{ % for c in config.list % }{ { c.title } }{ % endfor % }
```

`_data/metadata.json`:
```json
{"site":{"title":"DAX","url":"http://localhost:8080"}}
```
```dax
{ { metadata.title } }
{ { site.url } }
```

## SEO

`seo.dax` partial auto included:

```dax
<title>{ { title } } - { { metadata.title } }</title>
<meta name="description" content="{ { description } }">
<link rel="canonical" href="{ { site.url } }{ { url } }">
```

Auto generates:
- `/sitemap.xml`
- `/robots.txt`
- `/rss.xml`

## Public Assets

Everything in `public/` is copied to `site/`:

```
public/img/logo/logo.webp -> site/img/logo/logo.webp
public/css/style.css -> site/css/style.css
```

**IMPORTANT:** Always place images in `public/img/...` not `site/`.

Supported MIME types in dev server:
- `.css`, `.js`, `.json`, `.svg`, `.webp`, `.png`, `.jpg`, `.gif`, `.ico`, `.woff2`

## Bento Grid Example

`content/minimal.md`:

```yaml
---
layout: minimal.dax
bento1:
  title: Launch in 30 Seconds
  image: /img/logo/dax-csharp-2.webp
bento3:
  item:
    - icon: /img/icon/fast.svg
      title: Blazing Fast
---
```

## CLI Commands

```bash
dotnet run -- init   # create starter structure
dotnet run -- build  # build to site/
dotnet run -- start  # build + serve at :8080 with watcher
```

## Troubleshooting

**Image not loading?**
- Check file exists in `public/img/...`
- Check MIME type in `DaxServer.cs` `GetMimeType()`
- Rename files without `#`, spaces, `( )`

**Icon not showing?**
- Check `site/img/icon/fast.svg` exists after build
- Ensure `public/img/icon/` has files

**`{ % endif % }` leaking?**
- Update `DaxEngine.RenderIfs` to nested-safe version

**Layout vs Partial collision?**
- Layouts load from `templates/layouts/`
- Partials load from `templates/partials/`
- Engine now separated: `LoadLayout()` vs `LoadPartial()`

**Pagination prev/next broken on first/last?**
- Use `has_prev` / `has_next` boolean, not `prev_url != ""`

```dax
{ % if pagination.has_prev % }...{ % endif % }
```

## Credits

Built with pure .NET by AXcora.
CSS by Axcora CSS - Bento Grid System.
Inspired by 11ty and Jekyll.

Support: [https://github.com/sponsors/mesinkasir](https://github.com/sponsors/mesinkasir)
