# homepage

My browser homepage. One static HTML file, no external requests, no build step.

- **Live:** https://<project>.pages.dev (set after first deploy)
- **Hosting:** Cloudflare Pages, auto-deploys on push to `main`
- **Offline:** a service worker (`sw.js`) caches the page, so every load after
  the first is served from local disk — same speed as opening a `file://` copy.
- **Mobile:** responsive (4 cols → 2 → 1). The `localhost` section is hidden on
  phones. Add to Home Screen gives a standalone app icon.

## Editing

Edit `index.html` and push. Cloudflare rebuilds in ~15s.

```bash
git add -A && git commit -m "Add X to racing" && git push
```

After a content change the service worker serves the **old** page once, then
updates in the background — a second load shows the change. To force everyone
onto new content immediately, bump `CACHE = 'home-vN'` in `sw.js`.

## Structure

| File | Purpose |
|---|---|
| `index.html` | Everything — markup, CSS, the filter script |
| `sw.js` | Service worker (stale-while-revalidate cache) |
| `manifest.json` | PWA manifest for Add to Home Screen |
| `icon-*.png` | App icons |

## Filter

Start typing anywhere on the page to filter links by name or URL. `Enter` opens
the first match, `Esc` clears.
