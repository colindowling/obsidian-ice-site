# Obsidian ICE — static site

Single-page static site. No build step, no framework, no dependencies to install.
Drop the contents of this folder at the web root and it runs.

    index.html
    img/            14 assets (12 JPG, 2 MP4) — ~9 MB total

## Deploying

Any static host works (Netlify, Vercel, Cloudflare Pages, S3+CloudFront, nginx).
Serve `index.html` at `/` and keep `img/` beside it — all asset paths are relative.

Recommended server config:
- Long cache headers on `/img/*` (immutable, 1 year); short/no-cache on `index.html`
- gzip or brotli on HTML/CSS/JS (the images and video are already compressed)
- HTTP/2 or better

## External dependencies

One: Google Fonts (Outfit + IBM Plex Mono), loaded via `<link>` in the head.
To self-host instead, download both families, drop them in `/fonts`, replace the
`<link>` with `@font-face` rules, and keep the existing fallback stacks.

Nothing else is fetched from outside the origin.

## How the page works

- All CSS and JS are inline in `index.html`. No external .css or .js files.
- Scroll effects are driven by one rAF-throttled scroll handler, no libraries.
- Reveals are opt-in: the hidden state is applied by script only after it confirms
  IntersectionObserver is available and `prefers-reduced-motion` is not set.
  With JS off, or reduced-motion on, everything renders visible and static.
- Videos hold their source in `data-src` and only load within 500px of the
  viewport. Below 820px wide they are suppressed entirely and a poster shows.
- Single-theme by design (dark). There is no light mode.

## Before this goes live

1. **Email addresses** — `deals@`, `capital@`, `hello@` are placeholders.
2. **Contact form** — currently `preventDefault()` with an on-page acknowledgement;
   it does not transmit. Wire it to a real endpoint (Formspree, a serverless
   function, or your CRM) and replace the acknowledgement text.
3. **Securities disclosure** — the footer references an "appropriately registered
   broker-dealer". Have a securities attorney confirm the actual arrangement
   before launch if any fee is tied to capital raised.
4. **Imagery** — a mix of licensed stock and AI-generated frames. The figures in
   them are illustrative and are not Obsidian personnel; do not caption them as
   staff, crews or owned assets.
5. **Analytics** — none installed.
