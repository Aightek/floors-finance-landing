# HANDOFF - Floors Finance Modular Landing
_Last updated: 2026-03-11_

---

## Current State

- **Task:** Landing page visual enhancements — hero pills + newsletter animation
- **Phase:** Complete — five commits pushed this session
- **Branch:** `master` at commit `0525ae4`

## What We Did

Added animated hero pills to the "Next Generation of Onchain Assets" section conveying the floor vs market price concept. Then rebuilt the newsletter section from scratch with a unified animated line system — background S-curves flow continuously while two anchor lines (floor = green, market = white) draw in on scroll, with a premium fill between them and a per-letter spring title entrance.

## Decisions Made

- **Pills at `bottom: 88px`** — Mirrors the section's `padding-top: 100px` for visual balance. Positioned `absolute` inside `cta-main` (already `position: relative`).
- **Sequential pill focus animation** — 6s cycle, 2s per pill, `cubic-bezier(.4,0,.2,1)` ease-in / `cubic-bezier(.6,0,1,.6)` ease-out. Easing baked per keyframe segment, not on the `animation` shorthand. Accent green icon on the floor pill differentiates the guarantee from volatility.
- **Unified line visual language** — All lines (background + floor + market) use the same S-curve formula (`M 0,y C 232,y±w 464,y∓w 696,y-end`). Background paths flow; floor/market stay stationary. Rejected keeping separate chart vs background SVG systems.
- **Background path loop** — `stroke-dasharray: 120 520` (period = 640). `@keyframes nl-crawl { to { stroke-dashoffset: -640 } }` gives a perfect seamless loop. 19 paths with staggered `animation-delay` of `idx * 0.55s` so none sync.
- **Gradient locked to `gradientUnits="userSpaceOnUse"` with `y1=96 y2=182`** — Matches the actual y-range of the market/floor lines in the viewBox, not the full viewBox height. Makes the mint fill visibly gradient within the premium zone.
- **Premium fill timing** — `transition: opacity 0.8s ease 2.2s` (delay 2.2s after `nl-chart-go`). Market line finishes drawing at ~2.4s so fill begins just as lines complete.
- **Letter animation** — `cubic-bezier(.34,1.56,.64,1)` (spring with overshoot, matching 21st.dev BackgroundPaths). Words stagger at `wordDelay += 0.1s`, letters at `ci * 0.03s`.
- **Newsletter section height: 600px** — 2x the original natural height. Flex column + `align-items: center` keeps content vertically centered without absolute positioning.

## Code Changes

**Files modified this session:** `index.html` only

**Session commits:**
| Hash | Description |
|---|---|
| `a220bc2` | Add floor/market price pills to Next Generation section |
| `fa57b41` | Move cta-pills to absolute bottom of section |
| `0f631b9` | Sequential focus animation on pills + bottom padding to 88px |
| `3288c2b` | Full newsletter section rebuild with animated lines |
| `0525ae4` | Merge background lines with floor/market, 2x section height |

**Key selectors added:**
```
.cta-pills          — absolute bottom:88px, flex row, centered
.cta-pill           — pill badge (border, bg, muted text)
.cta-pill-icon      — 22px circle badge inside pill
.cta-pill-icon--accent — accent green variant for floor pill
@keyframes pill-focus  — 6s cycle: inactive → active → inactive
.nl-canvas          — absolute inset SVG, z-index:0
.nl-floor / .nl-market — stroke-dashoffset draw-in on .nl-chart-go
.nl-premium         — fill with transition delayed 2.2s after trigger
.nl-letter / .nl-word  — spring letter entrance on .nl-title-go
@keyframes nl-crawl — stroke-dashoffset -640 loop for bg paths
```

## SVG Line Positions (viewBox 0 0 696 316)

```
y=140  MARKET  white 0.5/1.2px  M 0,140 C 87,118 142,158 204,132 C ... C 618,92 657,108 696,102
y=182  FLOOR   accent green 1.5px  M 0,182 C 232,174 464,163 696,150

Background bands:
  Above market (y=140):  8, 24, 40, 56, 72, 88, 104, 120
  Between (y=140–182):   155, 163, 171
  Below floor  (y=182):  197, 213, 229, 245, 261, 277, 292, 308

Premium fill path:
  M 0,140 [market forward] 696,102 L 696,150 C 464,163 232,174 0,182 Z
```

## Open Questions

- [ ] Should labels ("market" / "floor") be added to the SVG at a safe x position (x≈300–400 to survive mobile crop)? Deferred — title text provides enough context for now.
- [ ] `cta-main` Lottie animation files (`HeroIntro.json` / `HeroLoop.json`) — still untracked, not deployed. Pills layer above `z-index:2` (same as Lottie layer) so z-order should be correct when files land.
- [ ] All CTA buttons still point to `#` — real dApp/dashboard URLs needed.
- [ ] Testnet page open items still pending (see below).

## Testnet Page Open Items (from previous session)

- [ ] Real CTA link destinations
- [ ] Live leaderboard data (currently hardcoded)
- [ ] Tier Distribution values show `—` dashes
- [ ] Footer version string `v1.4.2-ALPHA` — confirm
- [ ] Hero animation files for testnet — reuse `Hero.json` or separate

## Known Issues / Caveats

- **Mobile crop on newsletter SVG** — `preserveAspectRatio="xMidYMid slice"` crops x:254–442 at 375px screen. Background paths span full 0–696 so some are clipped at edges (fine, decorative). Floor/market lines also exist in center so always visible.
- **No hamburger nav at <800px** — design-system bug, affects `testnet.html` primarily.
- **Many untracked files** — `docs/`, `emails/`, `assets/images/`, `assets/illustrations/`, `assets/logos/partners/`, animation JSONs — not deployed, not in scope.

## Next Steps

1. [ ] Add visual/animation content (Lottie files) to sections once finalized
2. [ ] Wire real CTA links when dApp/dashboard URLs are available
3. [ ] Consider adding "market" / "floor" SVG labels at x≈320 (safe mobile zone)
4. [ ] Port newsletter animation to `testnet.html` if desired
5. [ ] Address testnet page open items (leaderboard, CTAs, tier values)
6. [ ] Confirm footer version string and copyright across both pages

## Files to Review on Resume

- `index.html` — all changes this session; search `cta-pills`, `nl-canvas`, `nl-chart-group`, `Newsletter floor/market animation`
- `testnet.html` — testnet-specific page, open items above
- `docs/design/design-system.html` — token/component/pattern reference

## Context Notes

- Static site, no build step
- Deploy: GitHub `master` → Vercel (`https://floors-finance-landing.vercel.app`)
- Constraint: preserve modular design system at all times — no standalone redesigns
- All animation JS lives inside one `DOMContentLoaded` listener in `index.html` ~line 1378
- `reduceMotion` variable checked at the top of the listener — all animations gate on it
- Design tokens: `--bg:#0a0a0a` `--border:#262626` `--text:#fafafa` `--muted:#a1a1a1` `--accent:#beffb0`
