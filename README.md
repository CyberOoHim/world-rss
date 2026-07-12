# WorldWire — Maintainable Edition

Single-page RSS reader where feeds are externalized for developer maintenance.

## Files
- `index.html` — the app (single file, PWA installable, works standalone)
- `feeds.json` — canonical source of truth, edit this to add/remove sources
- `feeds.js` — fallback for file:// opening (window.WORLDWIRE_FEEDS)

## How to maintain feeds
Edit feeds.json:

```json
{
  "My Category": [
    {
      "id": "my-blog",
      "name": "My Blog",
      "flag": "📰",
      "url": "https://example.com/rss.xml",
      "homepage": "https://example.com"
    }
  ]
}
```

- `id` must be unique, lowercase, no spaces
- `flag` is any emoji
- `url` must be direct RSS XML URL starting with http
- `homepage` is the site URL

Then reload the page or click Developer > Reload feeds.json. No rebuild needed.

## Deploy
Upload all 3 files to same folder on GitHub Pages / Netlify / any static host with HTTPS. The app will auto-detect feeds.json and become installable.

## PWA
When served over HTTPS, browser will offer Install. Service worker caches shell + feeds.json.

## Fallback
If feeds.json is missing (e.g., opening index.html alone from disk), app uses feeds.js if present, otherwise tiny embedded fallback so UI still loads.
