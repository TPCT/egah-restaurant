# EGAH update — 2026-11-11

Deployed supplied ZIP HTML update to https://egah.shiftcodes.net/ . All image files use jsDelivr pinned to cc0953ef5913fa2682a2ae27464f892beea832e4 in this repository. Existing WebP photos match the supplied JPG originals. Smaller 192px logo, 48px favicon and supplied QR published. Text/buttons remain HTML. Menu is https://egah-restaurant-cafe.yallaqrcodes.com/branch/1/ in both languages.

Performance: all 11 distinct assets returned 200, combined 711842 bytes; hero preload and CDN preconnect; QR lazy loading; artificial welcome reduced from 5000ms to 700ms (zero in reduced motion); slideshow advancement skips hidden/offscreen hosts. Public HTML transfers approximately 16KB compressed. No Lighthouse score measured.

Deployment: atomic index replacement, server/local SHA256 4065beb089f34b25578f6cbe2797f382c59f052e2e2250fdccdb4031ff296d38. Backup site and original EGAH vhosts: /root/egah-backups/20261111-update on shiftcodes-server. HTTP vhost now respects X-Forwarded-Proto=https to stop the pre-existing Cloudflare HTTPS redirect loop; TLS vhost unchanged. Public HTTPS200; public HTTP301 and direct-origin HTTP301. Apache configtest Syntax OK; unrelated pre-existing missing document-root warnings left untouched.

QA: both inline scripts pass node --check. Independent reviewer found no blockers. Internal browser: English/LTR and Arabic/RTL desktop (1265px) and mobile (390px), hero, communication links, food imagery, hours, footer; menu click opens actual restaurant menu. Zero broken loaded image tags, zero console errors in checked desktop run, no horizontal overflow at checked desktop/mobile widths. Phone/mail destinations inspected without placing calls or sending mail. Other external social destinations not exercised end to end. Reduced-motion arithmetic reviewed, device setting not exercised.

Browser root URL retained a cached redirect from the initial failure; network root is 200, acceptance used ?v=20261111 to bypass that cached redirect. The temporary preview was moved outside web root after acceptance. No Docker used; no LMS files modified.
