# 📰 Anti-Wall

A lightweight, distraction-free article reader you can host on GitHub Pages.
Paste any article URL and read it cleanly — no ads, no popups, no paywalls (soft ones at least).

**[→ Live demo](https://your-username.github.io/anti-wall/)**

## How it works

1. You enter a URL
2. The app fetches the page via a CORS proxy (with automatic fallback)
3. [Mozilla Readability](https://github.com/mozilla/readability) extracts the article content
4. The clean article is rendered in a distraction-free reader view

Everything runs in the browser — no server, no database, no backend.

## Features

- 🔗 **Shareable URLs** — `?url=https://...` links open the article directly
- 🌙 **Dark mode** — follows system preference
- ♻️ **Proxy fallback** — tries corsproxy.io → allorigins.win → codetabs.com
- 📱 **Responsive** — works on mobile

## Deploy to GitHub Pages

### Automatic (recommended)

1. Fork / clone this repository
2. Go to your repo **Settings → Pages**
3. Under *Source*, select **GitHub Actions**
4. Push to `main` — the workflow deploys automatically

### Manual one-time setup

```bash
git clone https://github.com/YOUR_USERNAME/anti-wall.git
cd anti-wall
git push origin main   # triggers the Action
```

The GitHub Action (`/.github/workflows/deploy.yml`) runs on every push to `main`
and deploys the static files using the official `actions/deploy-pages` action.

## Limitations

- **Hard paywalls** (server-side): if the site only sends a teaser and requires a login token,
  the proxy will fetch the same partial content.
- **Rate limits**: public CORS proxies have quotas; don't use for high-traffic production sites.
- **Blocked proxies**: some sites detect and block proxy IPs.

## Tech stack

| Tool | Role |
|---|---|
| HTML + CSS + Vanilla JS | Frontend (no framework) |
| [Mozilla Readability](https://github.com/mozilla/readability) | Article extraction |
| [jsDelivr CDN](https://www.jsdelivr.com/) | Readability.js delivery |
| corsproxy.io / allorigins.win | CORS proxy |
| GitHub Actions | CI/CD |
| GitHub Pages | Hosting |

## License

MIT
