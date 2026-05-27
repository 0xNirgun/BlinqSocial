# Deploy v2-glitch to Vercel

Two paths. Pick A if you want speed, B if you want the repo to be the site.

---

## A · Keep the subfolder, tell Vercel where to look

### 1. Push this project to GitHub

```bash
cd <this-project>
git init
git add .
git commit -m "blinq landing — glitch direction"
git branch -M main
git remote add origin git@github.com:<you>/blinq-landing.git
git push -u origin main
```

### 2. Import on Vercel

1. https://vercel.com/new → pick your repo → **Import**
2. Expand **Root Directory** → **Edit** → select `v2-glitch`
3. Framework Preset: **Other**
4. Build Command: *(empty)*
5. Output Directory: *(empty)*
6. **Deploy**

The `vercel.json` already in this folder handles the routes.

---

## B · Flatten to repo root

Use this if you want a clean repo that **is** the site.

```bash
# in a NEW empty directory
mkdir blinq-landing && cd blinq-landing
git init

# copy the whole v2-glitch folder contents in
cp /path/to/this-project/v2-glitch/*.html .
cp /path/to/this-project/v2-glitch/*.css  .
cp /path/to/this-project/v2-glitch/vercel.json .

git add .
git commit -m "blinq landing — full glitch system"
git branch -M main
git remote add origin git@github.com:<you>/blinq-landing.git
git push -u origin main
```

Then on Vercel: https://vercel.com/new → import → **Deploy** (no config needed; default settings work).

---

## Routes you get either way

| URL | serves | what it is |
|---|---|---|
| `/` | `surface-2.html` | Universal invite landing (@basedchad sent you) |
| `/refer/:commish` | `surface-2.html` | Universal invite |
| `/m/:slug` | `surface-1.html` | Market-share landing |
| `/referrals` | `surface-3-dashboard.html` | Commish dashboard (auth'd) |
| `/referrals/leaderboard` | `surface-4-leaderboard.html` | Public leaderboard |
| `/connect` | `surface-5-wallet-connect.html` | Wallet-connect states (Privy chrome) |
| `/post-trade` | `surface-6-post-trade.html` | Post-trade return overlay |
| `/onboarding` | `surface-7-onboarding.html` | First-time commish walkthrough |

The `:slug` and `:commish` are placeholders right now — when you wire up real
attribution, read them with `new URLSearchParams(location.search)` or pull
them from the path via your backend.

---

## CLI alternative (no GitHub needed)

If you'd rather skip GitHub entirely for the first push:

```bash
cd v2-glitch
npx vercel           # follow prompts, link to a new project
npx vercel --prod    # ship it
```

You can connect GitHub to the project later from the Vercel dashboard.

---

## Custom domain

Vercel → your project → **Settings → Domains** → add `blinq.fi` (or whatever).
DNS instructions appear there. Both the apex and `www` work out of the box.

---

## Files in this folder

```
surface-1.html               · /m/:slug  — market-share landing
surface-2.html               · /         — universal invite landing
surface-3-dashboard.html     · /referrals — commish dashboard (auth'd)
surface-4-leaderboard.html   · /referrals/leaderboard — public board
surface-5-wallet-connect.html · /connect — Privy modal states (4 variants)
surface-6-post-trade.html    · /post-trade — return overlay (3 variants)
surface-7-onboarding.html    · /onboarding — first-login flow (4 steps)

glitch.css                   · shared design system (S3–S7 reference it)
vercel.json                  · route rewrites
```

`surface-1.html` and `surface-2.html` keep their CSS inline and are
fully self-contained. Everything else pulls from `glitch.css`.

## What to update before going live

- [ ] Real brand fonts + logo (currently improvised — Space Grotesk + JetBrains Mono)
- [ ] Real Polymarket Gamma slugs for the markets list
- [ ] Real commish data (currently hard-coded @basedchad, leaderboard rows)
- [ ] Wire `connect →` button to Privy
- [ ] Wire dashboard auth state — currently it always shows logged-in @basedchad
- [ ] Replace `vercel.json` rewrites if you want true dynamic routing (e.g. SSR market data) — at that point you're upgrading to Next.js, not just static HTML
