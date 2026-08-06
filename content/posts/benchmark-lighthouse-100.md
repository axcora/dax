---
title: DAX Benchmark - 50ms Load, 0KB JS, Lighthouse 100
description: Performance benchmark DAX vs Blazor vs Hugo vs Jekyll - why 0KB JS matters for SEO
layout: minimal/post.dax
image: /img/microsoftssg.webp
date: 2026-07-28
tags: [performance, benchmark, lighthouse, seo]
---


## Benchmark

Same blog with 11 pages:

| Generator | Build Time | JS Payload | First Paint | Lighthouse |
|-----------|------------|------------|-------------|------------|
| DAX | 127ms | 0KB | 50ms | 100 |
| CAX (C) | 1.2s + gcc | 0KB | 50ms | 100 |
| Blazor | 8s | 512KB WASM | 2100ms | 78 |
| Jekyll | 2.1s + ruby | 15KB | 120ms | 92 |

### Why 0KB matters?

- No JS = no parse, no hydration, instant SEO crawl
- No WASM boot = no 2s blank screen
- CDN friendly, edge cache 100%

> DAX is not for apps. DAX is for content that must be fast and rank.

Slim philosophy: **No bloat, no node_modules, no overhead.**
