# HANDOFF - Floors Finance Modular Landing
_Last updated: 2026-03-12 (session 3)_

---

## Current State

**Task:** Landing page visual polish — floor-premium section
**Phase:** Complete — session 3 wrapped
**Branch:** `master` at commit `3ed0b16`

---

## What We Did (Session 3)

Built the `.floor-premium` section — a new explainer between `feature-rows` and `module-3col` that visualises the gap between floor and market price with the message "you can do whatever you want with your floor." Iterated three times: initial build → borderless cards with vertical dividers → icons removed (text only). Also cleaned all AI tool folders (`.windsurf`, `.roo`, `.continue`, etc.) from the project directory, and installed the `designer-skills` plugin globally via `claude plugin install`.

---

## floor-premium Section (new, session 3)

- **Placement:** Between `feature-rows` and `module-3col`
- **Background:** 30 lines parallel to floor curve, same system as footer-cta. Reference: `M -50,300 C 200,275 480,248 810,210`. White opacity `0.022+i*0.005`, stroke-width `0.3+i*0.018`, `stroke-dasharray: 260 1600`, `nl-crawl` animation, random negative delay.
- **Chart (viewBox 760×200):**
  - Floor line: `M 80,165 C 260,158 480,138 680,105` — accent green, draws in 2s
  - Market line: `M 80,145 C 130,112 165,150 225,118 C 282,86 312,128 372,96 C 432,64 458,104 518,78 C 568,56 622,86 680,62` — white 0.4, draws in 2.5s + 0.2s delay
  - Premium fill: market path closed back along floor — `#fp-grad` green gradient, fades in at 1.5s
  - "PREMIUM" label at x=380, y=128; dots + "market"/"floor" labels at x=688
- **Action cards:** 3-col grid, `gap:0`. Text only — no icons. Vertical `border-left` dividers between cards; flips to `border-top` on mobile.
- **Trigger:** IntersectionObserver 25% on section → adds `.fp-chart-go` to `.fp-chart-group`, `.fp-actions-go` to `.fp-actions`
- **Landmarks:** CSS `/* === Floor Premium section ===` · HTML `class="wrap frame floor-premium"` · JS `// ── Floor Premium section`

---

## footer-cta State (session 2, unchanged)

- **Section class:** `.footer-cta`
- **Background:** 30 lines parallel to floor curve `M -50,283 C 250,253 500,208 750,143`. White opacity, `stroke-dasharray: 260 1600`, random negative `nl-crawl` delay.
- **Chart (trigger: 25% scroll):**
  - Premium fill, floor line (accent green, 1.8s), market line (white 0.4, 2.2s + 0.2s delay)
  - Chart y-range: 168–240 in 316px viewBox
  - End-point dots + "market"/"floor" labels at x=497
- **Title:** "Your floor. Your move." — per-letter spring entrance `cubic-bezier(.34,1.56,.64,1)`
- **Section:** `min-height: 440px`, flex column centered

---

## cta-pills (session 2, unchanged)

Three pills at bottom of `.cta-main`, `position: absolute; bottom: 88px`. Sequential focus animation: 6s cycle, 2s per pill. Stagger: 0s / 2s / 4s.

| Pill | Icon | Treatment |
|---|---|---|
| Market price fluctuates | Jagged chart | `.cta-pill` default |
| Floor price only ever rises | Rising floor + arrow | `.cta-pill-icon--accent` (green bg) |
| Your floor — sell, borrow, or hold | Infinity | `.cta-pill` default |

---

## What Was Tried and Rejected

- **Unified horizontal line system** (`0525ae4`) — 19 horizontal S-curves for footer-cta background. User preferred diagonal aesthetic — reverted.
- **Card icons in floor-premium** — tried, removed. Text only is cleaner.

---

## Open Questions / Next Steps

- [ ] **floor-premium copy** — "Your floor was always the worst case." (Sell card) may need a tone pass
- [ ] **footer-cta tweaks** — labels at x=497 may clip on mobile; fill opacity; line weight
- [ ] **footer-cta section height** — `min-height: 440px`, may need adjustment
- [ ] **Lottie files** — `Hero.json`, `Curve.json`, etc. untracked. Stack order correct when they land (`z-index:1` Lottie, `z-index:2` pills)
- [ ] **All CTA links** — point to `#`, real URLs needed
- [ ] **testnet.html** — hardcoded leaderboard data, `—` tier distribution, `#` links, `v1.4.2-ALPHA` unconfirmed

---

## Key Files

- `index.html` — all changes; search `cta-pills`, `nl-canvas`, `nl-chart-group`, `Footer CTA floor/market animation`, `floor-premium`, `fp-chart-group`
- `testnet.html` — separate page, open items above
- `docs/design/design-system.html` — token/component/pattern reference

---

## Context / Constraints

- Static site, no build step — vanilla HTML/CSS/JS only
- Deploy: `master` → Vercel at `https://floors-finance-landing.vercel.app`
- Modular design system must be preserved — no standalone redesigns
- All animation JS in one `DOMContentLoaded` listener in `index.html` ~line 1387
- `var reduceMotion` checked at top of listener — all animations must gate on it
- Design tokens: `--bg:#0a0a0a` `--border:#262626` `--text:#fafafa` `--muted:#a1a1a1` `--accent:#beffb0`
- Font: Poppins 400/500/600

---

## Session Commits

| Hash | Description |
|---|---|
| `a220bc2` | Add floor/market price pills to Next Generation section |
| `0f631b9` | Sequential focus animation on pills + bottom: 88px |
| `3288c2b` | Full newsletter section rebuild (FloatingPaths + chart) |
| `77e9084` | Restore newsletter to 3288c2b state |
| `9f7dff5` | footer-cta: rename + chart shift up 50px |
| `4309b0c` | card-with-media: scale 80%, top-aligned |
| `1ec8277` | faq: add hook panel |
| `3148f58` | footer-cta bg: parallel to floor curve |
| `c580148` | footer-cta bg: random start positions |
| `a5eb500` | floor-premium: add section |
| `53f9a20` | floor-premium: borderless cards with dividers, parallel bg lines |
| `3ed0b16` | floor-premium: remove action card icons, text only (HEAD) |
