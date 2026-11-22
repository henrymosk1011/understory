# Understory

**Live: https://henrymosk1011.github.io/understory/**
Source: https://github.com/henrymosk1011/understory

Agency-grade organic growth infrastructure — a static marketing site with a
landing page, sign-in and access-request screens.

![Hero](docs/preview-hero.png)

The design was reverse-engineered from `https://realgrowth.app` with REA:
the original's markup and stylesheet were captured over HTTP and the rendered
page was captured in a real Chromium session. The layout, design system and
copy structure follow that site; the brand, wordmark and mark are original.

## Stack

None. Static HTML, one stylesheet, one script. No build step, no dependencies,
no framework — GitHub Pages serves the files as-is.

## Structure

```
index.html                 landing page: hero, thesis, engine, capabilities, proof, pricing, FAQ, CTA
login.html                 sign-in screen
register.html              access-request screen
assets/css/styles.css      the whole design system
assets/js/main.js          header state, scroll reveal, particles, drawer, anchors, demo form note
assets/images/favicon.svg  seedling mark
docs/*.png                 renders of the live site
```

## Design system

| Token | Value | Use |
| --- | --- | --- |
| ink-base | `#070908` | page |
| ink-card | `#0c1411` | pricing cards |
| ink-elev | `#11181a` | feature hover |
| char | `#a3e635` | accent: buttons, rules, italic display |
| char-bright | `#c5f25a` | primary hover |
| cream | `#f4f0e6` | headings, body |
| cream-dim / faint | `rgba(244,240,230,.62 / .30)` | secondary copy |
| ash | `rgba(244,240,230,.09)` | hairlines |

Fraunces (variable serif, `opsz`/`SOFT`) for display, Geist for body, JetBrains
Mono for eyebrows, numerals, buttons and labels. Container `1280px`, gutter
`clamp(24px, 5vw, 72px)`, section rhythm `clamp(96px, 14vw, 200px)`.

Four stacked fixed atmosphere layers: a canvas particle field (64 drifting
motes, 32 under 700px), SVG-noise grain at 6% in `overlay` blend, a radial
vignette, and a multi-stop radial page gradient.

## Behaviour

- Header compacts and gains a blurred bar after 40px of scroll.
- Sections and the three engine steps fade/rise in via `IntersectionObserver`.
- Mobile drawer below 960px: numbered nav, `Esc` to close, body scroll lock.
- Anchor links offset by 80px so the fixed header never covers a heading.
- Hero headline and CTA animate in on load, staggered.
- `prefers-reduced-motion: reduce` disables particles, reveals and transitions.
- Breakpoints: 960 / 880 / 760 / 560 / 540 / 380px.

## Not real

The sign-in and register forms have **no backend** — submitting prints
"Demo only — this form has no backend" and nothing is sent. There is no auth,
session, billing or dashboard. Prices, the "240+ agencies" figures and the FAQ
answers are demo content, not claims about a real company.

## Deploying

GitHub Pages, `main` / root:

```bash
git push                      # Pages rebuilds automatically
gh api repos/:owner/understory/pages/builds/latest --jq .status
```

Any static host works the same way — there's nothing to compile.

## Provenance

Captured 2026-11-22 from `https://realgrowth.app/`:

- `GET /` → 200, `text/html`, 23,984 bytes
- `GET /inc/themes/default/assets/css/lander.css?v=20260505g` → 200, 33,562 bytes
- `GET /inc/themes/default/assets/js/lander.js?v=20260505d` → 200, 4,992 bytes
- Chromium 157 render: hero at 1440×900 (DSR 2), thesis section, and the network
  log (document, CSS, JS, Google Fonts, Cloudflare RUM beacon — no app API).

The original is a server-rendered PHP app behind Cloudflare; this is a static
reimplementation. Custom "R" mark replaced with an original seedling mark.
