# T1 — Serve images from jsDelivr CDN (WebP)

Size: S. File: `index.html` only. Do NOT touch anything under `images/`.

## Context
Optimized WebP copies of all images are already committed and live on jsDelivr, pinned to commit
`c1a2cda6c8e04bfdd67ee58f34fbced71e4a3890`:

    https://cdn.jsdelivr.net/gh/TPCT/egah-restaurant@c1a2cda6c8e04bfdd67ee58f34fbced71e4a3890/images/<name>.webp

Available: burger, chicken-burger, chicken-parmesan, interior, seabass, steak, terrace, tiramisu, logo-400 (all `.webp`).
`images/qr-call.svg` stays local (tiny). Google Fonts stay as is.

## Changes
1. CSS `--img: url("images/X.jpg")` (hero, duo, hours, closer, sea) → the CDN `.webp` URL.
2. Every `<img src="images/logo-512.png">` → CDN `logo-400.webp`; add `decoding="async"` and explicit `width`/`height` where missing is NOT required (CSS sizes them).
   Keep the `<link rel="icon">` favicon pointing to local `images/logo-512.png` (favicons should stay same-origin PNG).
3. Slideshow JS (`d.dataset.src = 'images/' + src.trim();` around line 792): build URLs from one constant
   `var IMG_BASE = 'https://cdn.jsdelivr.net/gh/TPCT/egah-restaurant@c1a2cda6.../images/';` (full SHA) and
   change all `data-slides="a.jpg,b.jpg"` attributes to `.webp` names.
4. In `<head>`: `<link rel="preconnect" href="https://cdn.jsdelivr.net" crossorigin>` and
   `<link rel="preload" as="image" href="<CDN>/interior.webp" fetchpriority="high">` (hero LCP image).
5. No other refactors, no formatting churn.

## Acceptance
- `grep -nE "images/[a-z-]+\.(jpg|png)" index.html` only matches the favicon line.
- No remaining `.jpg` names in `data-slides`.
- Page has no JS errors; every CDN URL used returns 200 (verify with curl for each distinct URL).
