# HANDOFF — Floors Finance Modular Landing
_Last updated: 2026-03-09_

---

## Project Overview
Static single-page landing page for Floors Finance, built in vanilla HTML/CSS/JS with no build step. Primary working file is `index.html`; testnet page is `testnet.html`; motion assets are in `Animations/`. Deploy flow is GitHub `master` to Vercel (`Aightek/floors-finance-landing`). No `CLAUDE.md` exists in project root.

## Current Status
Latest pushed commit: `18fedbb` (`Add testnet landing page; remove hidden sections from main`)

Completed this session:
- Created `testnet.html` — full dedicated testnet landing page
- Wired `index.html` Testnet nav link → `testnet.html`
- Removed hidden `.testnet` section from `index.html` (product cards, was `display:none`)
- Removed hidden `.leaderboard` section from `index.html` (was `display:none`, had UTF-8 mojibake)
- Reviewed `Floors UI/UX & CRO Overview.md` — a UX/CRO audit document with quick wins and high-impact items still pending

## testnet.html Structure (top → bottom)
1. **Nav** — Logo → `index.html`, "Testnet" link marked `.is-active`
2. **Hero** — Pulsing "Genesis Testnet Live" status dot, `h1` "Floor Only Goes Up", testnet sub-copy, "Enter dApp" (primary) + "Check Dashboard" (secondary) CTAs; shares HeroIntro/HeroLoop Lotties
3. **Protocol Pillars** — 6-card 3×2 grid: Guaranteed Floor, Always Liquid, Interest-Free, Auto-Scaling, Permissionless, Cross-Chain
4. **Stat Divider** — "748 participants. 140,000 points distributed. Phase One is live."
5. **Genesis Rewards / Leaderboard** — `display:grid` (not hidden); live pulsing dot; 10 clean wallet entries (UTF-8 fixed); 4 tasks; tier values show `—` instead of `0`
6. **Benefits** — 5 product cards (Presale, Hold, No Liquidations, Volatility, Supply)
7. **Feature Rows** — 5 animated panels (F1–F5 Lotties), same hover/IntersectionObserver logic as main
8. **FAQ** — 6 flip cards: floor price definition, liquidation risk, how floor rises, genesis rewards, audit, Phase One end
9. **CTA** — "Join Genesis Phase One", "Enter dApp" primary + email capture inline
10. **Footer** — Same 4-column grid as main

## Key Decisions
- Testnet page is a standalone HTML file (not a route/SPA) — consistent with zero-build-step project
- Hidden `.testnet` and `.leaderboard` sections fully removed from `index.html` DOM — no dead weight
- Leaderboard wallet data replaced with clean readable aliases (`floors.eth`, `0x4f3c…a12e`, etc.) — original data was double-UTF-8 encoded mojibake, unrecoverable
- Tier distribution shows `—` instead of `0` — signals "data pending" rather than "zero participants in tiers"
- Hero on testnet reuses same Lottie assets (`HeroIntro.json` / `HeroLoop.json`) — avoids new asset dependency
- `prefers-reduced-motion` guard included on all Lottie and animation code
- Pulse animation added to `.hero-status-dot` and `.lb-live-dot` via `@keyframes pulse-dot`

## UX/CRO Audit — Pending Items
The file `Floors UI/UX & CRO Overview.md` contains a full audit. Items NOT yet implemented:

**Quick Wins (low effort, high impact):**
- [ ] Surface audit link near hero CTA as a trust badge
- [ ] Rewrite newsletter section headline ("Feel the difference" → value-exchange copy)
- [ ] Downgrade "Read Documentation" CTA to text link (index.html hero)
- [ ] Style "Launch App" nav button as accented action

**High-Impact:**
- [ ] Mobile navigation menu (hamburger/drawer at ≤800px) — both pages
- [ ] Move partner logo strip above the fold (below hero) on index.html
- [ ] Replace partner text names with actual logo assets from `Partner Logos/` folder
- [ ] Hero headline rewrite on index.html to pass 5-second clarity test

**Known Issues Carried Forward:**
- `prefers-reduced-motion` guard missing on hero Lottie in `index.html` (covered in testnet.html)
- Partner logos folder `Partner Logos/` is untracked — needs decision: commit or gitignore
- `Floors UI/`, `design-system.html`, `article.md`, `image.png`, `Email-Logo.svg` all untracked at root — triage needed

## Blockers / Caveats
- Git history still contains `Co-Authored-By: Claude Sonnet 4.6` lines in older commits. Can be rewritten with `FILTER_BRANCH_SQUELCH_WARNING=1 git filter-branch --msg-filter 'sed "/^Co-Authored-By:/d"' -- --all` followed by `git push --force` if desired.
- No in-browser visual QA run this session — testnet.html is code-complete but unverified at runtime.

## Next Steps
1. Visual QA `testnet.html` in browser — verify Lottie animations load, leaderboard layout, FAQ flips, CTA email capture.
2. Visual QA `index.html` — confirm removal of hidden sections didn't shift any layout.
3. Implement quick wins from UX audit: audit badge, CTA hierarchy, newsletter headline.
4. Implement mobile nav (hamburger/drawer) — affects both `index.html` and `testnet.html`.
5. Swap partner text names for real logos from `Partner Logos/` folder.
6. Triage untracked root files — commit useful ones, gitignore the rest.

## Context Notes
- Design tokens: `--bg: #0a0a0a`, `--text: #fafafa`, `--muted: #a1a1a1`, `--accent: #beffb0`, `--border: #262626`, `--col-pad: 44px`
- Grid language: `.frame` (border, no border-top), `.wrap` (max 1060px), `repeat(3,1fr)` columns, `min-height: 304px` cells
- Mechanic cards live at `index.html` around `.mechanic-card` / `.mechanic-copy` (3 cards, 608px height, gradient overlay via `::before`)
- FAQ section: `.faq` / `.faq-cell` / `.faq-card` — pure CSS 3D Y-flip on hover
- Hero verb cycling: `initHeroHeadlineRotation()` in JS, sequence `['Hold','Trade','Borrow','Loop','Earn']`, 2000ms interval
- `.hook-highlight` is used only on the "Floors fixes this" paragraph inside `.hook-panel`
- Commit messages do NOT include `Co-Authored-By` lines (user preference)
- Lottie lib loaded from CDN: `cdnjs.cloudflare.com/ajax/libs/bodymovin/5.12.2/lottie.min.js`
