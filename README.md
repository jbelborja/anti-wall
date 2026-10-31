# 📰 Anti-Wall

A lightweight, distraction-free article reader hosted 100% on **GitHub Pages**.
Paste any article URL and read it cleanly — no ads, no popups, no soft paywalls.

**[→ Live demo](https://jbelborja.github.io/anti-wall/)**

## How it works

1. You enter a URL.
2. The app fetches the page using a multi-tiered client-side proxy and extraction chain.
3. [Mozilla Readability](https://github.com/mozilla/readability) extracts the core article content and strips clutter.
4. Clean, readable article is rendered in a distraction-free view.

Everything runs directly in your browser — **no Cloudflare, no backend server, no database, and zero configuration required**.

## Proxy & Fallback Chain

To bypass browser CORS restrictions and bot-blockers without running your own server, Anti-Wall uses an intelligent multi-step fallback chain:

| Priority | Source | How it works |
|---|---|---|
| **1** | `corsproxy.io` | Fast CORS proxy for standard sites |
| **2** | `allorigins.win` | Secondary public CORS fallback |
| **3** | `codetabs.com` | Tertiary public CORS fallback |
| **4** | **Jina Reader** (`r.jina.ai`) | Serverless reader service that bypasses bot protection |
| **5** | **Wayback Machine** (`archive.org`) | Fetches snapshots for older or blocked articles |
| **6** | **Interactive Fallbacks** | 1-click bypass buttons in UI (Archive.today, 12ft.io, Wayback) |

## Deploy to GitHub Pages

No external accounts or workers to set up:

1. Fork or clone this repository.
2. In your repo on GitHub, go to **Settings → Pages**.
3. Under **Build and deployment**, set **Source** to **GitHub Actions**.
4. Push to the `main` branch — the GitHub Action deploys the site automatically!

## Tech stack

| Tool | Role |
|---|---|
| HTML5 + CSS3 + Vanilla JS | Frontend (zero build step, zero npm dependencies) |
| [Mozilla Readability](https://github.com/mozilla/readability) | Article extraction |
| Public CORS & Reader APIs | Client-side fetch & bot bypass |
| GitHub Actions | CI/CD deployment |
| GitHub Pages | Static hosting |

## License

MIT
