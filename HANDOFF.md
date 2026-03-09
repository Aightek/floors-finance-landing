# HANDOFF — Floors Finance Modular Landing
_Last updated: 2026-03-09_

---

## Project Overview
Static single-page landing page for Floors Finance, built in vanilla HTML/CSS/JS with no build step. Primary working file is `index.html`; motion assets are in `Animations/`. Deploy flow is GitHub `master` to Vercel (`Aightek/floors-finance-landing`). No `CLAUDE.md` exists in project root.

## Current Status
Latest pushed commit: `ad15256` (`Darken gradient behind mechanic card text`)

Completed this session:
- Renamed mechanic cards: "Built-In Liquidity" → "Always-On Liquidity", "Native Borrowing" → "Liquidation-free Borrowing"
- Reordered mechanic cards: Liquidity | Rising Floor Price | Borrowing
- Fixed hero gap: removed `min-width: 6ch` from `.hero-verb`
- Added fade+slide transition to hero verb word cycling (180ms ease, out↑ / in↓)
- Updated hero sub copy → "DeFi with Rising Floor Prices" (24px)
- "Floors fixes this at the asset level." is now a standalone `<p class="hook-highlight">` — green (`--accent`), underlined, 22px
- Updated all three mechanic card descriptions with new copy
- Added FAQ section (3-column card grid, 304px cells) with 3D Y-axis flip on hover — front shows question centered, back shows answer
- Mechanic card titles changed from `h3` → `h4`
- Mechanic card height: 680px → 608px
- "Rising Floor Price" title uses `<br>` to force 2-line wrap; liquidity description uses `<br>` for 4-line wrap
- `min-height` locks on `h4` (2 lines) and `p` (4 lines) keep all three cards vertically balanced
- Gradient overlay on mechanic cards: `::before` on `.mechanic-copy`, fades transparent → 85% dark → `var(--bg)`, improves text contrast over Lottie animations

## Key Decisions
- FAQ built as native card grid (not accordion) to stay consistent with design system's `repeat(3,1fr)` / 304px / 44px pad / border-grid language
- FAQ flip interaction is pure CSS (`transform-style: preserve-3d`, `backface-visibility: hidden`) — no JS
- Mechanic card gradient uses `rgba(10,10,10,.85)` midpoint rather than a hard stop, so the animation is still visible above the text area
- `min-height` on `h4`/`p` uses `calc()` against font-size × line-height × line-count — keeps balance without hardcoding px
- Commit messages no longer include `Co-Authored-By` lines (user explicitly requested removal; history rewrite was attempted but blocked — history still contains old lines, user is aware)

## Blockers / Caveats
- Git history still contains `Co-Authored-By: Claude Sonnet 4.6` lines in older commits. A `git filter-branch` + force push was attempted but blocked mid-session. Can be revisited with `FILTER_BRANCH_SQUELCH_WARNING=1 git filter-branch --msg-filter 'sed "/^Co-Authored-By:/d"' -- --all` followed by `git push --force`.
- No in-browser visual QA was run this session; all changes are code-complete but unverified at runtime.

## Next Steps
1. Revisit Co-Authored-By history rewrite if desired (see Blockers above).
2. Visual QA mechanic cards at ~1060px: verify gradient coverage, 608px height, Lottie fit.
3. Visual QA FAQ section: confirm 3D flip works smoothly, back-face text is readable.
4. Check `prefers-reduced-motion` — FAQ flip has `transition: none` guard; hero verb transition does not yet.
5. Triage untracked root files (`Floors UI/`, `Partner Logos/`, `design-system.html`, `article.md`, images) — keep or remove.
6. Optional: remove unreferenced `Illustrations/Price_Floor.svg`.

## Context Notes
- Design system tokens: `--bg: #0a0a0a`, `--text: #fafafa`, `--muted: #a1a1a1`, `--accent: #beffb0`, `--border` (dark border), `--col-pad: 44px`
- Grid language: `.frame` (border, no border-top), `.wrap` (max 1060px), `repeat(3,1fr)` columns, `min-height: 304px` cells
- Mechanic cards live at `index.html:1079–1107` (`.mechanic-card` / `.mechanic-copy`)
- FAQ section lives at `index.html` around the `.faq` / `.faq-cell` / `.faq-card` block, between partners and newsletter sections
- Hero verb cycling: `initHeroHeadlineRotation()` in JS, sequence `['Hold','Trade','Borrow','Loop','Earn']`, 2000ms interval, `swapVerb()` handles CSS class transitions
- `.hook-highlight` is used only on the "Floors fixes this" paragraph inside `.hook-panel`
