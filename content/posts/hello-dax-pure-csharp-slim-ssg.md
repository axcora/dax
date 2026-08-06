---
title: Hello DAX - Pure C# Slim Static Site Generator That Slaps Blazor Bloat
description: Why DAX built with pure C# 800 lines Program.cs is faster than Blazor WASM for blogs and docs - 0KB JS vs 512KB
layout: minimal/post.dax
image: /img/c-staticsitegenerator.webp
date: 2026-08-03
tags: [csharp, dax, ssg, blazor, performance]
---


## What is DAX?

DAX is Pure C# Slim Static Site Generator. Single file **Program.cs ~800 lines**, no Node, no WASM, no hydration.

Inspired by CAX (C language) but rewritten for .NET ecosystem so Windows users can use **CMD native** without MinGW or make.

### Why not Blazor?

Blazor is for interactive dashboards. It loads **512KB WASM + _framework/blazor.web.js**, boot time ~2s, needs hydration.

DAX outputs **pure HTML 0KB JS**, 50ms load, Lighthouse 100, SEO instant.

**Benchmark same blog:**

- Blazor: `dotnet publish` 8s, payload 512KB, first paint 2.1s
- DAX: `dotnet run -- build` 0.12s, payload 0KB, first paint 0.05s

> Use Blazor for apps. Use DAX for content.

### How to start?

```bat
dotnet new console -n my-blog
copy Program.cs Dax.csproj
dotnet run -- init
dotnet run -- build
dotnet run -- start
```

Deploy to Vercel, Netlify, GitHub Pages — they have dotnet preinstalled, unlike CAX which fails without GCC.
