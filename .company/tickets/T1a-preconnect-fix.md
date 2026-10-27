# T1a — Review fix: preconnect without crossorigin
Size: S. File: `index.html` only.
In `<head>`, change `<link rel="preconnect" href="https://cdn.jsdelivr.net" crossorigin>` to
`<link rel="preconnect" href="https://cdn.jsdelivr.net">` — images and CSS backgrounds are no-cors requests, so a
CORS-mode preconnect is never reused. Change nothing else. Acceptance: that line has no `crossorigin`; diff is one line.
