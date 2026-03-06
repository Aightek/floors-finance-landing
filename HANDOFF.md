# HANDOFF — Floors Finance Modular Landing
_Last updated: 2026-03-06_

---

## Project Overview
Static single-page marketing site for Floors Finance (DeFi protocol), built entirely in vanilla HTML/CSS/JS in [`index.html`](./index.html). No framework, no build step. Animations live in `Animations/`. Deploy: GitHub → Vercel, branch `master` (`Aightek/floors-finance-landing`). No `CLAUDE.md` in project root.

## Current Status
**Completed this session:** All 5 feature row visuals are now implemented. Features 2–5 were empty spacer cells; all are now filled with animated stat cards matching the Feature 1 visual language.

Latest commit: `d9e2802` — pushed to `master`, Vercel auto-deploy triggered.

**Feature card summary** (all markup + CSS in `index.html`):
- **Feature 1** (~lines 882–910): Floor Price card — existing, unchanged
- **Feature 2** (~lines 912–950): "Your Position" — entry `$0.30` vs floor `$0.42`, scaleX gap bar
- **Feature 3** (~lines 961–995): "Borrow Health" — Safe status + green health bar fill
- **Feature 4** (~lines 996–1047): "Reserve Growth" — `+2.4%` + sequential fee ticker rows
- **Feature 5** (~lines 1048–1090): "Supply & Backing" — SVG ring stroke + `1.24x` ratio

CSS blocks for Features 2–5 at ~lines 413–515 (inserted after the Feature 1 reduced-motion block).

JS: shared `initFeatIllustration(id, animClass)` factory at ~line 1236, triggers Features 2–5 via IntersectionObserver.

No blockers.

## Key Decisions
- **Reused `.feat1-card`, `.feat1-shell`, `.feat1-card-meta`, `.feat1-card-k/v` classes** for Features 2–5 rather than duplicating CSS — only unique visual elements per feature get new classes (`feat2-*`, `feat3-*`, etc.)
- **`transform: scaleX()` not `width` for progress bars** (Features 2 & 3) — per UX guideline: animate composited properties only
- **`stroke-dashoffset` for SVG ring** (Feature 5) — composited, smooth 60fps
- **Sequential `animation-delay`** for fee ticker rows (Feature 4) — 0.45s / 0.65s / 0.85s, creates live-feed feel without JS
- **No infinite decorative animations** — Feature 3 dot is static green, not pulsing (UX: infinite animations are distracting)
- **`threshold: 0.25`** for IntersectionObserver on Features 2–5 (vs 0.35 on Feature 1) — slightly earlier trigger since cards have more content

## Next Steps
1. **Visual QA all 5 cards** at desktop (1060px) and ensure truncation/clipping feels intentional — check `top: 32px` and `height: 320px` on `.feat1-card` (shared by all features)
2. **Finalize copy/values** — all numbers (`$0.42`, `$840`, `42M`, etc.) are placeholder-realistic; confirm before launch
3. **Rename stale CSS comment** at ~line 324: `/* -- Feature 1: HUD Area Chart Illustration */` → update to reflect current card implementation
4. **Mobile audit** — `.feature-spacer { display: none }` hides all 5 visuals on mobile; verify text panels read well standalone
5. **Triage untracked root files** — `Floors UI/`, `Partner Logos/`, `article.md`, `design-system.html`, `email-msxv6.html` — decide include vs delete
6. **Consider creating `CLAUDE.md`** now that stable patterns exist worth persisting across sessions

## Context Notes
- All feature visuals share `.feat1-card` CSS (`position: absolute`, `top: 32px`, `height: 320px`, `opacity: 0` default). Each feature's animate class (`.feat[N]--animate .feat1-card`) sets `opacity: 1; transform: translateY(0)`.
- Keep exactly one `id="feat1-visual"` — `initFeatureOneIllustration()` depends on it.
- `initFeatIllustration` factory runs **after** `initFeatureOneIllustration()` and **before** the `if (!window.lottie) return` guard — order matters.
- Feature 4 fee ticker uses pure CSS `@keyframes feat4Tick` — no JS needed.
- Feature 5 SVG ring: `r="26"`, circumference `2π×26 ≈ 163`. `stroke-dashoffset: 41` ≈ 75% fill. Adjust to change fill level.
- `prefers-reduced-motion` coverage: Feature 1 at ~line 407; Features 2–5 at ~lines 434–437.
