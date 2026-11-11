# EGAH update implementation plan

Goal: Deploy the supplied November update to egah.shiftcodes.net with all image files on a CDN and working text/actions.
Architecture: Existing static HTML on Apache, Cloudflare front door, commit-pinned jsDelivr images from TPCT/egah-restaurant. Preserve supplied content and reuse identical existing optimized WebP photos. No Docker.

- [x] Publish supplied QR, small favicon and appropriately sized logo assets; verify all CDN responses.
- [x] Apply supplied HTML update, replace image and slideshow paths with pinned CDN URLs, preload hero, shorten artificial five-second intro, stop offscreen slideshow downloads.
- [x] Validate inline JS and source links, review diff independently.
- [x] Back up site and affected Apache vhosts outside web root. Resolve reproduced Cloudflare HTTPS loop with proxy-aware redirect, retain direct HTTP redirect and TLS. Scope to EGAH only.
- [x] Publish atomically, verify public responses/compression, desktop/mobile English/Arabic screenshots and actions in internal browser. Record evidence and rollback path.

Decision: User delegated CDN selection; use existing owned public repository and jsDelivr. Keep fonts on existing Google CDN. No new hosting service or paid plan.
