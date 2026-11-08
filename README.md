# ELLIDE — landing page

Stealth landing page for [ellide.com](https://ellide.com). One file, no build step, no dependencies.

## Contents

| File | Purpose |
|---|---|
| `index.html` | The entire site: markup, styles, WebGL shader, wordmark SVG and favicon are all inline |
| `CNAME` | Tells GitHub Pages to serve the site at `ellide.com` |

## What the page does

- Petrol background (`#0F3640`) with a live bathymetric contour field rendered in WebGL — depth lines that drift like a current.
- Pointer acts as a lens: the field bends toward it and the lines brighten.
- Click or tap drops a ripple that displaces the contours. An ambient ripple fires every 7–16 s when idle.
- The wordmark's letters lean toward the cursor; the nearest one lifts. Letters land one by one on load.
- `hello@ellide.com` copies to clipboard on click, with `mailto:` as fallback.
- Honours `prefers-reduced-motion`. Falls back to a static gradient if WebGL is unavailable.

## Brand constants

| Token | Value |
|---|---|
| Petrol (background) | `#0F3640` |
| Mist (wordmark, lines) | `#B7C9CC` |
| Light | `#F0F4F4` |
| Wordmark geometry | 928 × 100 units, 18-unit stroke, three-bar E, Ð with 47.9 × 50 outer bowl |

The wordmark SVG inside `index.html` is the master vector; copy it from there rather than re-tracing.

## Editing

Open `index.html` in any editor. Things most likely to change:

- **Email address** — appears twice: the `<a id="mail">` link text/href, and the `writeText(...)` call in the script.
- **Line density** — `float k=14.;` in the fragment shader (higher = more contours).
- **Line strength** — `float strength=mix(.075,.16,idx);` (regular, index line).
- **Drift speed** — the `u_t*.012` / `u_t*.008` terms in `vec2 q=...`.

Preview locally by opening the file in a browser; no server needed.

## Deploy

Hosted on GitHub Pages from the `main` branch root. Pushing to `main` publishes within a minute.

DNS for `ellide.com` points at GitHub Pages:

```
A      @    185.199.108.153
A      @    185.199.109.153
A      @    185.199.110.153
A      @    185.199.111.153
CNAME  www  <github-user>.github.io
```

Email for `@ellide.com` is handled separately via MX records; this repo only serves the web page.
