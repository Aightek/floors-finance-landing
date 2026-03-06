# HANDOFF — Floors Finance Modular Landing
_Last updated: 2026-03-06_

---

## Project Overview
Static single-page marketing site for Floors Finance (DeFi protocol), built entirely in vanilla HTML/CSS/JS in [`index.html`](./index.html). No framework, no build step. Animations live in `Animations/`. Deploy: GitHub → Vercel, branch `master` (`Aightek/floors-finance-landing`). Design system reference: [`design-system.html`](./design-system.html) (untracked, use for component tokens).

## Current Status
**Completed this session:** Full redesign of all 5 feature card visuals + addition of eyebrow labels to feature text panels.

Latest commit: `3097ab1` — pushed to `master`, Vercel auto-deploy triggered.

**Feature card visuals** (all markup + CSS in `index.html`):
- **F1** (~line 851): Floor Price — staircase SVG line art, `$0.42`, "Only moves up"
- **F2** (~line 868): Your Position — Entry/floor before-after rows + large `+40%` hero
- **F3** (~line 899): Borrow Health — outlined `● Safe` pill badge + collateral/borrowed split
- **F4** (~line 927): Reserve Growth — upward sparkline SVG + `+$3,600` single number
- **F5** (~line 953): Supply & Backing — large centered ring (110px), `1.24x` overlaid

**Feature panel labels** — `.f-label` eyebrow above each `h4`:
- Price Floor / Downside Protection / Zero Liquidations / Fee Capture / Supply Backing
- CSS at ~line 491: `color: var(--accent)`, `font-size: 14px`, `letter-spacing: -.28px`, `margin-bottom: 24px`
- Matches design system `.t-label` / Accent Label token (see `design-system.html` line 103, 286, 617)

**Card background:** Removed — transparent, border only (`1px solid rgba(255,255,255,0.14)`).

No blockers.

## Key Decisions
- **Removed 2×2 stat grids from all 5 cards** — primary clutter source; each card now has one focal visual element
- **Each card uses a distinct concept** (staircase / before-after / status badge / sparkline / ring) — not variations of same template; Vercel-style minimal
- **Card background set to transparent** — `background: transparent` on `.feat1-card`, border only
- **`.f-label` uses design system Accent Label token** (`color: var(--accent)`, `14px`, `letter-spacing: -.28px`) — sourced from `design-system.html` line 617, not custom
- **Card padding increased 18px → 24px, gap reduced 12px → 6px** — more breathing room per Vercel reference
- **F5 ring enlarged**: radius 38 (was 26), `stroke-dasharray: 239`, 110px SVG (was 66px) — centered layout with flex: 1
- **Accent color restrained** — used on single key value per card only

## Next Steps
1. **Visual QA** — check all 5 cards at 1060px desktop; verify card truncation (`.feat1-card` is `position: absolute`, `top: 32px`, `height: 320px`)
2. **F4 sparkline** — currently uses `preserveAspectRatio="none"` which stretches the line; consider `xMidYMid meet` if it looks distorted at narrow widths
3. **Finalize copy/values** — `$0.42`, `$840`, `$210`, `+$3,600`, `1.24x` are placeholder-realistic; confirm before launch
4. **Mobile audit** — `.feature-spacer { display: none }` hides all visuals on mobile; verify text panels + `.f-label` + `h4` read well standalone
5. **Stale CSS comment** at ~line 324: still says `/* -- Feature 1: HUD Area Chart Illustration */` — rename to reflect current card
6. **Triage untracked root files** — `Floors UI/`, `Partner Logos/`, `article.md`, `design-system.html`, `email-msxv6.html` — decide include vs delete
7. **Consider `CLAUDE.md`** — stable patterns now exist worth persisting

## Context Notes
- All 5 feature visuals share `.feat1-card` CSS (position absolute, top 32px, height 320px, opacity 0 default). Animate class per feature sets `opacity: 1; transform: translateY(0)`.
- JS factory `initFeatIllustration(id, animClass)` at ~line 1236 handles F2–F5 via IntersectionObserver. Order matters: runs after `initFeatureOneIllustration()`, before `if (!window.lottie) return`.
- F5 ring: `r="38"`, circumference ≈ 239. `stroke-dashoffset: 60` ≈ 75% fill. Adjust to change level.
- F1 staircase SVG uses hardcoded `#beffb0` (same as `--accent`) — if accent token changes, update SVG stroke/fill manually.
- `design-system.html` is untracked — safe to read for token reference but don't commit unless intentional.
- `prefers-reduced-motion` coverage: F1 at ~line 407; F2–F5 at ~line 436 (only `.feat5-ring-fill--lg` transition suppressed now; old bar/gap classes removed).
