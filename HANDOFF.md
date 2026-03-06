# HANDOFF — Floors Finance Modular Landing
_Last updated: 2026-03-06_

---

## Project Overview
This project is a static single-page marketing site for Floors Finance, built with vanilla HTML/CSS/JS in [`index.html`](/e:/WORKS/Floors%20Finance/Modular%20Landing/index.html). Animation assets live in `Animations/`. Deploy flow is GitHub -> Vercel on branch `master` (`Aightek/floors-finance-landing`).

There is no `CLAUDE.md` in project root and no `.planning/` directory this session.

## Current Status
Feature 1 (first right-side visual cell in `.feature-rows`) was fully redesigned from chart-based HUD variants into a **truncated stat-card visual** focused on Floor Price.

Current implementation (all in [`index.html`](/e:/WORKS/Floors%20Finance/Modular%20Landing/index.html)):
- Feature 1 CSS block around lines ~324–412 now styles `.feat1-card` instead of SVG line chart animation classes.
- Feature 1 markup around lines ~773–804 uses:
  - `Floor Price` label
  - `$0.42` value
  - `Guaranteed minimum value`
  - compact details grid (`Reserve Backed`, `Daily Rise`, `Status`, `Floor Mode`)
- Card is intentionally clipped/truncated from bottom and moved higher with `top: 32px`.
- Reveal behavior is still one-shot via `initFeatureOneIllustration()` around lines ~963–985.

No blockers in code execution. Main open work is visual tuning and content/format confirmation.

## Key Decisions
- Chose **stat-card metaphor** over chart metaphor for Feature 1 because user preferred a clearer “Floor Price” cue over abstract line art — see `.feat1-card` and Feature 1 markup in [`index.html`](/e:/WORKS/Floors%20Finance/Modular%20Landing/index.html).
- Chose **bottom-truncated card composition** to preserve visual intrigue while fitting the feature cell — controlled via `.feat1-shell` overflow + `.feat1-card` positioning.
- Chose **minimal but meaningful detail set** (`Reserve Backed`, `Daily Rise`, `Status`, `Floor Mode`) to fill vertical space without making the card dense.
- Kept implementation in **plain HTML/CSS** (no component libraries/framework changes) to match project stack and avoid introducing dependencies.
- Used Pencil MCP once to inspect `Landing.pen` node `LkOxA`, then reverted from that direction after user feedback.

Recent commit sequence relevant to Feature 1:
- `b4cb83b` align to `LkOxA`
- `236d7e1` revert to pre-`LkOxA`
- `36b2eee` replace with truncated Floor Price card
- `24e0146` increase card detail density and raise card
- `e30a0fb` set top offset to 32px
- `2662ef8` increase meta vertical spacing

## Next Steps
1. Visual QA the current Feature 1 card in desktop/tablet and ensure truncation amount feels intentional (check `.feat1-card` `top/height` in [`index.html`](/e:/WORKS/Floors%20Finance/Modular%20Landing/index.html)).
2. Decide final copy/values for stats (`$0.42`, `+0.6%`, etc.) to avoid placeholder-like production content.
3. Rename stale section comment `/* -- Feature 1: HUD Area Chart Illustration ... */` to match current card implementation (it is outdated and may confuse future edits).
4. Implement Feature 2–5 visuals in remaining empty `.feature-spacer` cells with consistent visual language (card-based or chart-based, but unified).
5. Triage untracked root files/directories (`Floors UI/`, `Partner Logos/`, `article.md`, `design-system.html`, etc.) and decide inclusion vs cleanup.

## Context Notes
- Keep exactly one `id="feat1-visual"`; animation trigger depends on it.
- Mobile hides `.feature-spacer` (line ~625), so Feature 1 visual does not render on mobile; only text panel remains.
- `HANDOFF.md` was stale before this update; use this version as source of truth.
- Repository currently has unrelated untracked files; commits in this session intentionally scoped to `index.html` plus `HANDOFF.md`.
- If `.pen` inspection is needed again, prefer Pencil MCP tools (as done for `LkOxA`) rather than hand-reading `.pen` internals.
