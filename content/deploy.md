---
layout: minimal/page.dax
title: Deploy
description: Deploying DAX to Everywhere
---

DAX generates pure static HTML to `site/`. That means it deploys ANYWHERE - no runtime, no Node, no .NET on server.

> Build command everywhere: `dotnet run -- build` or `bin/DAX build`
> Publish directory: `site`

---

## 1. GitHub Pages (Recommended - Free)

DAX includes a ready workflow `.github/workflows/deploy.yml`.

### Steps:
1. Push your DAX project to GitHub (main branch)
2. Go to Repo > Settings > Pages > Source: **GitHub Actions**
3. Push to main - auto deploy in 30s

Workflow does:
```yaml
setup-dotnet 9.0
dotnet publish -o bin
dotnet run -- build
upload ./site to Pages
```

Your site will be at `https://username.github.io/dax/`

**Custom domain?** Add `public/CNAME` file with `yourdomain.com`

---

## 2. Vercel (Fastest - Edge)

Vercel auto-detects static but needs build command.

### Option A: Vercel Dashboard
- Import GitHub repo
- Framework Preset: **Other**
- Build Command: `dotnet publish -c Release -o bin && dotnet bin/DAX.dll build`
  - or if you commit DAX binary: `./bin/DAX build`
- Output Directory: `site`
- Deploy

### Option B: vercel.json
Create `vercel.json` in root:
```json
{
  "buildCommand": "dotnet run -- build",
  "outputDirectory": "site",
  "framework": null
}
```

Vercel has .NET runtime, so `dotnet run` works. No `node_modules`.

---

## 3. Netlify (Simple + Forms)

### Netlify Dashboard:
- New site from Git
- Build command: `dotnet run -- build`
- Publish directory: `site`

### netlify.toml (recommended):
```toml
[build]
  command = "dotnet publish -c Release -o bin && bin/DAX build"
  publish = "site"

[build.environment]
  DOTNET_VERSION = "9.0"
```

**Bonus:** Netlify Forms still work - add `data-netlify="true"` to `<form>` in your `.dax` templates.

---

## 4. Cloudflare Pages (Fast + Free Unlimited Bandwidth)

Cloudflare Pages supports .NET via `dotnet` build.

### Steps:
1. Cloudflare Dashboard > Workers & Pages > Create > Pages > Connect Git
2. Build settings:
   - Build command: `dotnet run -- build`
   - Build output directory: `site`
   - Root directory: `/`
3. Environment variable: `DOTNET_VERSION = 9.0.0`

### Or Wrangler:
```bat
npx wrangler pages deploy site --project-name=dax
```

**Why Cloudflare?** Free, no bandwidth limit, edge cache global, perfect for DAX static HTML.

---

## 5. Manual Deploy (Any VPS / Nginx)

```bat
dotnet publish -c Release -o bin
bin\dax.exe build
:: upload site/* to /var/www/html/
```

Nginx:
```nginx
server {
  root /var/www/dax/site;
  location / { try_files $uri $uri/index.html =404; }
}
```

---

## Comparison

| Platform | Build Time | Bandwidth | Dotnet Needed | Cost |
|----------|------------|-----------|---------------|------|
| GitHub Pages | ~45s | 100GB | No (CI builds) | Free |
| Vercel | ~30s | 100GB | Yes (auto) | Free |
| Netlify | ~40s | 100GB | Yes | Free |
| Cloudflare | ~25s | Unlimited | Yes | Free |

**Recommendation:** GitHub Pages for docs/blogs, Cloudflare for high traffic.

---

## FAQ

**Q: Why not Blazor GitHub Pages deployment?**
A: Blazor needs WASM + `_framework/` 1-2MB JS. DAX output is < 50KB per page, loads in 50ms vs 2s.

**Q: Does Vercel/Netlify support `dax.exe`?**
A: Yes, publish DAX as single file: `dotnet publish -r linux-x64 --self-contained`. But easier use `dotnet run -- build`.

**Q: How to handle base path `/repo/` on GitHub Pages?**
A: Set `site.url` in `_data/metadata.json` to `https://username.github.io/repo/` and use `{{ site.url }}` in templates. Or use relative URLs.

---

## Deploy Checklist

- [ ] `dotnet run -- build` works locally, `site/` has `index.html`
- [ ] `.gitignore` ignores `bin/`, `obj/`, `site/` (but CI will rebuild `site/`)
- [ ] `_data/metadata.json` has correct `url`
- [ ] `site/sitemap.xml` exists (auto generated)
- [ ] Push to `main`
