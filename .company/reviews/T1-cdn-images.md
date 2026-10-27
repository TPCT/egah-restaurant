# Review — T1 (+T1a) serve images from jsDelivr CDN

Verdict: APPROVED (after T1a fix).

- Diff limited to index.html: CSS `--img` vars, logo `<img>`s, slideshow `IMG_BASE` + `.webp` data-slides, preconnect + hero preload. Favicon stays local PNG; qr-call.svg stays local.
- Finding (fixed in T1a): preconnect had `crossorigin`, which is never reused by no-cors image requests.
- CDN URLs pinned to commit c1a2cda6 — immutable, so jsDelivr can cache long-term. New images require a new SHA.

Evidence (2026-10-27):
- Codex: `node --check` on inline scripts passed; curl of all 9 CDN URLs → 200.
- Browser (local static server): hero + scrolled sections render; resources loaded from cdn.jsdelivr.net
  (interior 84KB, logo-400 44KB, seabass 110KB, tiramisu 101KB, terrace 110KB, burger 43KB); 0 broken <img>; 0 console errors.
- Image weight: 1.73MB (JPG/PNG) → 0.71MB (WebP, max 1200px).
