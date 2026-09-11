---
layout: cyber.dax

hero: 
  info:  50MS BUILD • PURE C# SLIM • BALZOR KILLER
  title1: BUILT IN
  title2: C#
  title3: NOT WASM.
  description: 
     info1: Pure C# static site generator. Single file Program.cs 800 lines. No Node, no Blazor WASM, no hydration. 
     info2: dotnet run -- build
     info3: 11 pages in 120ms.
  intro: DAX Dotenet by AXcora
  button_primary: 
    text: dotnet run -- build
    url: "#download"
  button_secondary: 
    text: Why not Blazor?
    url: "#compare"
  list: 
    - info: 0KB JS
    - info: 50ms Load
    - info: CMD Native
    - info: SEO Ready
    - info: MIT

features: 
  info: FEATURES — ZERO BLOAT
  title: Everything you need, nothing you don't.
  card: 
    - title: AUTO SEO
      text: "Auto SEO injection script generates sitemap.xml, robots.txt, rss.xml, meta tags, og:image, twitter:card. No config needed."
    - title: AUTO COLLECTIONS
      text: "content/services/jas.md → { { collections.services } } auto. No config, Jekyll style but faster."
    - title: JAMTSACK CONCEPT
      text: "Working with content/, templates/, public/ like Jekyll, Hugo, Eleventy. No Node, no Blazor, no hydration."
    - title: FREE NESTED FRONTMATTER
      text: "hero: list: [{name,url,meta:{deep:{level:3}}}] unlimited depth, no fixed schema."
    - title: TAGS + PAGINATION
      text: "tags: [csharp] → /tags/csharp/ auto. pagination:6 → /posts/page/2/"
    - title: YAML + JSON AUTO
      text: "_data/*.yaml, *.json → { { config.list }}, { { metadata.title }} directly in templates."
    - title: 0KB HYDRATION
      text: "Pure HTML output. No blazor.web.js, no WASM, Lighthouse 90+, instant SEO."
    - title: CMD NATIVE
      text: "Windows CMD, Linux, macOS. No MinGW, no make. Just dotnet SDK."

compare: 
  info: COMPARE DAX VS BLAZOR
  title: .NET is heavy. DAX is not.
  
get_start: 
  info: GET STARTED
  title: Build your site in 6 steps.
  card: 
    - title: CONFIGURATION
      text: "Open on _data/metadata.yaml and update site_url, title, description, author, social links and other settings."
    - title: STATIC PAGE
      text: "To create a static page, add a .md file in content/ folder. example content/about.md → /about/"
    - title: COLLECTION POSTS
      text: "To create a collection item, add a .md file in the collection's folder. example content/posts/hello.md → /posts/hello-dax/"
    - title: COLLECTION PAGE
      text: "To create a collection page, add a .md file in content/ folder. example content/posts.md → /posts/"
    - title: PUBLIC FOLDER
      text: "To add static assets, put them in public/ folder. example public/css/style.css → /css/style.css"
    - title: DEPLOY PROJECT
      text: "To deploy your project, upload the site/ folder to your hosting. example vercel.json, netlify.toml, .github/workflows/deploy.yml are ready to use."

docs: 
  info: DOCUMENTATION — FULL GUIDE
  title: Complete DAX docs

download: 
  title: Run and Try DAX SSG.
  description: MIT open source. Pick minimal (empty) or full blog template. Both work with dotnet run -- build.
  starter: 
    info: MINIMAL STARTER
    title: Clean Minimalis Starter
    text: "Get started in seconds. The official clean, minimal starter for DAX SSG — production-ready with _data/, content/, templates/, and public/ pre-configured. - 0KB JS. 50ms Load. Pure HTML + Axcora CSS. No bloat."
    text2: Built for scale. Clean output, semantic HTML, and best practices baked in from day one.
    button: 
      text: Run DAX Starter Minimal
      url: /minimal/
  premium: 
    info: DAX PRO
    title: Premium DAX Architecture Service
    image: /img/c-staticsitegenerator.webp
    text: "Build your project with custom DAX architecture. From bespoke UI and advanced features to full AI and API integration — we handle it all. Our expert team is ready to turn your vision into reality. Let's solve your project challenges and build for a better future."
    button: 
      text: Consult Now
      url: mailto:hi@axcora.com
    button2: 
      text: Hire Now
      url: https://www.fiverr.com/creativitas/create-your-custom-website-and-app

deploy: 
  title: DEPLOY ANYWHERE
  list: 
    - title: ▲ Vercel
      text: site/
    - title: ◍ Netlify
      text: site/
    - title: ⬢ GitHub Pages
      text: deploy.yml
    - title: ☁ Cloudflare
      text: unlimited bw

support:
  title1: Stop shipping 500KB
  title2: to show a blog.
  info: Support DAX with Buy a cup of coffee
  text: DAX is MIT. Clone, 
  run: dotnet run -- build
  text1: deploy. No WASM, no JS framework, just HTML that loads in 50ms.
  paypal: 
    text: Support Via PayPal
    url: https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=JVZVXBC4N9DAN
  gumroad: 
    text: Support Via Gumroad
    url: https://creativitaz.gumroad.com/coffee
  github: 
    text: Support Via Github
    url: https://github.com/sponsors/mesinkasir
---
