---
title: Deploy DAX to Vercel, Netlify, GitHub Pages and Cloudflare - No GCC Needed
description: How to deploy DAX pure C# SSG to modern hosts - works because dotnet preinstalled
layout: minimal/post.dax
image: /img/dotnetstaticsite.webp
date: 2026-07-29
tags: [deploy, vercel, netlify, github-pages]
---


## Vercel

`vercel.json`:

```json
{
  "buildCommand": "dotnet publish -c Release -o bin && ./bin/Dax build",
  "outputDirectory": "site"
}
```

## Netlify

`netlify.toml`:

```toml
[build]
  command = "dotnet publish -c Release -o bin && ./bin/Dax build"
  publish = "site"
```

## GitHub Pages

`.github/workflows/deploy.yml` builds with `actions/setup-dotnet@v4`, then upload `site/` artifact to `deploy-pages`.

## Why DAX not CAX?

Vercel / Netlify **have dotnet** preinstalled, **no GCC**. CAX `make` fails. DAX builds 127ms and deploys.

Cloudflare Pages same — output `site/`.
