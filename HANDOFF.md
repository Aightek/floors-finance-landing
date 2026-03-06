# HANDOFF — Floors Finance Modular Landing
_Last updated: 2026-03-06_

---

## Project Overview
Static single-page marketing site for Floors Finance (DeFi, rising floor-price mechanics), built in vanilla HTML/CSS/JS. Main implementation is in `index.html`; motion assets are in `Animations/`; deployment is Vercel via GitHub `master`. `Landing.pen` is the design reference and should be accessed via pencil MCP tools only. No `CLAUDE.md` or `.planning/` directory exists.

## Current Status
Feature 1 illustration was upgraded this session to a more Vercel-style grid module treatment in `index.html`.
- Reworked Feature 1 CSS into a structured “grid block” visual system with guides/crosshair/depth layering (`index.html` around lines 324+).
- Replaced the old small chart SVG with a larger, layered illustration inside the first feature spacer (`index.html` around line 848).
- Added early `initFeatureOneIllustration()` so Feature 1 animation no longer depends on Lottie availability (`index.html` around lines 1071–1093).
- Added reduced-motion handling for Feature 1 animation paths/effects (same CSS block).
- Removed duplicate legacy observer logic at script tail (single trigger path now).

No hard blocker during implementation, but visual QA in-browser is still pending in this session (desktop + mobile behavior confirmation). Current git state includes one modified tracked file: `index.html`.

## Key Decisions
- Chose a **Vercel-like grid-cell composition** (guides + cross anchors + clipped card surface) over the previous plain SVG panel because it creates clearer spatial structure and perceived polish while staying within vanilla stack — see Feature 1 CSS/markup in `index.html`.
- Kept **SVG + CSS animation** (not Lottie) for feature spacers, because these modules are static layout slots and lightweight one-shot draw animations are sufficient.
- Moved Feature 1 init **before Lottie guard** (`if (!window.lottie) return;`) so the illustration still animates even if CDN/script fails.
- Set observer threshold to **0.35** for Feature 1 trigger, aligned to “animate once when meaningfully in view,” then disconnect.
- Added **prefers-reduced-motion fallback** to disable scan/pulse and instant-set transitions for accessibility.

## Next Steps
1. Validate Feature 1 visually in browser at desktop and tablet widths; check clipping and contrast in the new shell (`index.html` Feature 1 block).
2. Confirm mobile intent: feature spacers are hidden on mobile (`.feature-spacer { display: none; }`), so Feature 1 visual is desktop-only.
3. Implement Features 2–5 illustrations in remaining empty `.feature-spacer` cells, reusing the new Feature 1 structural pattern where appropriate.
4. Run a quick animation sanity pass across existing Lottie sections to ensure no regressions from script-order changes.
5. Triage untracked assets (`Email-Logo.svg`, `Illustration.svg`, `Partner Logos/`, `email-msxv6.html`, `article.md`, `image.png`, etc.) and decide commit/integration scope.

## Context Notes
- Only one `feat1-visual` instance should exist in final markup (currently true); avoid accidental duplicate insertion when patching by line ranges.
- Keep labels in illustration SVG as `font-family="monospace"` to match site aesthetic.
- The new Feature 1 implementation is intentionally layered and subtle; avoid adding continuous infinite decorative motion.
- `HANDOFF.md` previously contained encoding artifacts in older content; keep files UTF-8 when editing to avoid malformed characters.
- `.pen` workflow constraint remains: do not read `Landing.pen` directly; use MCP tool calls.
