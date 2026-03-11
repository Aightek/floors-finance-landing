# HANDOFF - Floors Finance Modular Landing
_Last updated: 2026-03-11 (session 2)_

---

## Current State

**Task:** Landing page visual enhancements — footer-cta section iteration
**Phase:** Active
**Branch:** `master`

## What We Did

Added animated hero pills to the "Next Generation of Onchain Assets" section. Rebuilt the newsletter section with a FloatingPaths-style background + centred floor/market chart that draws in on scroll. Attempted a second newsletter variant that merged the background paths with the chart lines into one unified system, but user preferred the original `3288c2b` version — reverted at end of session.

## Current footer-cta State

- **Section class:** `.footer-cta` (renamed from `.newsletter`)
- **Background:** 30 diagonal FloatingPaths-style paths (15 each direction), fanning from off-screen top-left to off-screen bottom-right. Generated in JS on DOMContentLoaded. Stroke opacity 0.025–0.13, stroke-width 0.3–0.67. `stroke-dasharray: 260 1600`, `nl-crawl` keyframe `to { stroke-dashoffset: -1900 }`, duration 20–33s staggered.
- **Chart (trigger: 25% scroll into view):**
  - Premium fill: `M 200,230 C 232,198 ... 490,170 L 490,190 C 390,215 290,230 200,240 Z` — fades in at 1.5s delay
  - Floor line: `M 200,240 C 290,230 390,215 490,190` — accent green, draws in 1.8s
  - Market line: `M 200,230 C 232,198 258,242 292,214 C ... 490,170` — white 0.4 opacity, draws in 2.2s + 0.2s delay
  - End-point dots + "market" / "floor" labels at x=497 — fade in at 1.6s / 1.8s
  - Chart y-range: 168–240 in 316px viewBox (shifted up 50 units from previous 218–290, leaves bottom padding)
- **Title:** "Your floor. Your move." — per-letter spring entrance (`cubic-bezier(.34,1.56,.64,1)`), triggered same time as chart
- **Section:** `min-height: 440px`, flex column centered, `position: relative; overflow: hidden`

## What Was Tried and Rejected

- **Unified horizontal line system** (`0525ae4`) — replaced diagonal FloatingPaths with 19 horizontal S-curves (`M 0,y C 232,y±w 464,y∓w 696,y-end`) spanning full section width. Floor (y=182) and market (y=140) were anchor lines at section centre, background lines flowed above/below/between. `stroke-dasharray: 120 520`, loop period 640px. User preferred the original diagonal aesthetic — reverted via `git checkout 3288c2b -- index.html`.

## cta-pills (complete, no changes pending)

Three pills at the bottom of `.cta-main` ("Next Generation of Onchain Assets"), `position: absolute; bottom: 88px`:

| Pill | Icon | Treatment |
|---|---|---|
| Market price fluctuates | Jagged chart line | `.cta-pill` default (muted) |
| Floor price only ever rises | Rising floor + arrow | `.cta-pill-icon--accent` (green bg) |
| Your floor — sell, borrow, or hold | Infinity symbol | `.cta-pill` default |

Sequential focus animation: 6s cycle, 2s per pill. `@keyframes pill-focus` — ease in `cubic-bezier(.4,0,.2,1)` at 0→10%, linear hold 10→26%, ease out `cubic-bezier(.6,0,1,.6)` at 26→34%, inactive 34→100%. Stagger: pill 1 at `0s`, pill 2 at `2s`, pill 3 at `4s`.

## Decisions Made

- **Pills `bottom: 88px`** — mirrors `padding-top: 100px` on the section title for visual symmetry
- **Accent green on floor pill icon only** — distinguishes the "guaranteed" pill from the two informational ones without over-styling
- **Newsletter: diagonal FloatingPaths preferred over horizontal** — more atmospheric, less "charty". The chart lines (x: 200–490) are centred in the section and clearly separated from the fanning background.
- **Revert via `git checkout <commit> -- file`** — cleaner than `git revert` (which conflicted) or force-push

## Session Commits

| Hash | Description |
|---|---|
| `a220bc2` | Add floor/market price pills to Next Generation section |
| `fa57b41` | Move cta-pills to absolute bottom of section |
| `0f631b9` | Sequential focus animation on pills + bottom: 88px |
| `3288c2b` | Full newsletter section rebuild (FloatingPaths + chart) |
| `0525ae4` | Merge background lines with floor/market (REVERTED) |
| `a3d86ce` | Update HANDOFF |
| `77e9084` | Restore newsletter to 3288c2b state |
| _(next)_ | Rename newsletter→footer-cta, shift chart up 50px |

## Open Questions / Next Steps

- [ ] **footer-cta iteration** — chart position improved; may still want tweaks (label positions, section height, fill opacity, line weight)
- [ ] **Chart x-range** — lines currently x: 200–490 (centred safe zone for mobile). Labels at x=497 may clip on narrow viewports — consider moving to x=340 area or removing
- [ ] **footer-cta section height** — currently `min-height: 440px`. May need adjustment now that chart sits higher.
- [ ] **Lottie files** — `Hero.json`, `Curve.json`, `Leveraged.json` etc. are untracked. `cta-main` Lottie layer is `z-index:1`, pills are `z-index:2` — stack order is correct when files land.
- [ ] **All CTA links** point to `#` — real URLs needed
- [ ] **Testnet page** — leaderboard data hardcoded, tier distribution shows `—`, CTA links `#`, footer version `v1.4.2-ALPHA` unconfirmed

## Key Files

- `index.html` — all changes; search `cta-pills`, `nl-canvas`, `nl-chart-group`, `Footer CTA floor/market animation` (~line 1491)
- `testnet.html` — separate page, open items above
- `docs/design/design-system.html` — token/component/pattern reference

## Context / Constraints

- Static site, no build step — vanilla HTML/CSS/JS only
- Deploy: `master` → Vercel at `https://floors-finance-landing.vercel.app`
- Modular design system must be preserved — no standalone redesigns
- All animation JS inside one `DOMContentLoaded` listener in `index.html` ~line 1379
- `var reduceMotion` checked at top of listener — all animations must gate on it
- Design tokens: `--bg:#0a0a0a` `--border:#262626` `--text:#fafafa` `--muted:#a1a1a1` `--accent:#beffb0`
- Font: Poppins 400/500/600
