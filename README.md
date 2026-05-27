# Blinq Season 1 — Referral Landing Pages

Two design directions, both fully responsive (375 → 1280+), zero build step,
deployable as static to Vercel.

## What's here

```
design-review.html      ← side-by-side comparison canvas (open this first)

v1-terminal/            ← Direction A. Phosphor green on near-black, full
  surface-1.html          IBM Plex Mono, scanlines, ASCII chrome.
  surface-2.html
  vercel.json

v2-glitch/              ← Direction B. Brutalist editorial. Space Grotesk
  surface-1.html          display + JetBrains Mono numerals. Magenta /
  surface-2.html          lime / cyan with RGB-shift accents.
  vercel.json
```

- `surface-1.html` → market-share landing (`/m/[slug]?c=[commish]`)
- `surface-2.html` → universal invite landing (`/refer/[commish]`)

## Deploy to Vercel

Pick a direction folder and ship it.

```bash
cd v2-glitch          # or v1-terminal
vercel deploy --prod
```

The included `vercel.json` rewrites `/m/[slug]` → `surface-1.html` and
`/refer/[commish]` → `surface-2.html` and points `/` at the universal
invite page. Both pages are pure static HTML/CSS — only external
dependency is Google Fonts.

## Wiring up real data (next step)

The static pages have stubbed:

- Commish handle (`@basedchad`) + avatar initials
- Polymarket market data (Argentina to repeat as 2026 WC champion, etc.)
- Season 01 counters (days, vol attributed, commish count, pool size)
- Leaderboard rows
- Live ticker

When you hook this to the real backend / Polymarket Gamma API, the markup
exposes `class="num"` and `font-variant-numeric: tabular-nums` on every
number so live updates won't jitter.

## What's not here

Only Surfaces 1 + 2. Surfaces 3–7 (commish dashboard, public leaderboard,
wallet-connect, post-trade return, onboarding flow) plus empty/loading/
error states are next. Pick a direction and I'll extend it.
