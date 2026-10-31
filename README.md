# 📰 Anti-Wall

A lightweight, distraction-free article reader hosted on GitHub Pages.
Paste any article URL and read it cleanly — no ads, no popups, no soft paywalls.

**[→ Live demo](https://jbelborja.github.io/anti-wall/)**

## How it works

1. You enter a URL
2. The app fetches the page via a proxy with browser-like headers
3. [Mozilla Readability](https://github.com/mozilla/readability) extracts the article
4. Clean article is rendered in a reader view

Everything runs in the browser — no server, no database (optional Cloudflare Worker for tough sites).

## Why a Cloudflare Worker is needed for some sites

Sites like **elpais.com** use DataDome bot protection. They fingerprint the HTTP request and reject
anything that doesn't look like a real browser session — including all public CORS proxies.

A **Cloudflare Worker** runs on Cloudflare's edge network with real IPs and can send proper
browser headers, which bypasses most bot-detection systems. The free tier (100,000 req/day) is
more than enough for personal use.

## Deploy the Cloudflare Worker (recommended)

### Step 1 — Create the Worker

1. Go to [dash.cloudflare.com](https://dash.cloudflare.com/) → **Workers & Pages** → **Create**
2. Choose **"Hello World"** template → give it a name (e.g. `anti-wall`)
3. Replace the entire editor content with the code from [`worker/index.js`](worker/index.js)
4. Click **Deploy**
5. Copy the worker URL, e.g. `https://anti-wall.YOUR-NAME.workers.dev`

### Step 2 — Add your GitHub Pages domain to the allowlist

In [`worker/index.js`](worker/index.js), update the `ALLOWED_ORIGINS` array:
```js
const ALLOWED_ORIGINS = [
  'https://YOUR-USERNAME.github.io',
  'http://localhost',
];
```

### Step 3 — Set the worker URL in the app

In [`index.html`](index.html), find this line near the top of the `<script>` block:
```js
const WORKER_URL = ''; // e.g. 'https://anti-wall.YOUR-NAME.workers.dev'
```
Replace the empty string with your worker URL:
```js
const WORKER_URL = 'https://anti-wall.YOUR-NAME.workers.dev';
```

Then push — GitHub Actions redeploys automatically.

## Deploy to GitHub Pages

1. Fork / clone this repo
2. Go to **Settings → Pages → Source → GitHub Actions**
3. Push to `main` — the Action deploys automatically

## Proxy fallback chain

| Priority | Source | Works for |
|---|---|---|
| 1 | Your Cloudflare Worker | Most sites including DataDome-protected |
| 2 | corsproxy.io | Sites without aggressive bot detection |
| 3 | allorigins.win | Fallback |
| 4 | codetabs.com | Fallback |
| 5 | Wayback Machine | Articles archived > a few hours ago |

## Tech stack

| Tool | Role |
|---|---|
| HTML + CSS + Vanilla JS | Frontend (zero dependencies, zero build step) |
| [Mozilla Readability](https://github.com/mozilla/readability) | Article extraction |
| Cloudflare Workers (optional) | Browser-header proxy |
| GitHub Actions | CI/CD |
| GitHub Pages | Hosting |

## License

MIT
