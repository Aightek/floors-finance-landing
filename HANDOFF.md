# HANDOFF - Floors Finance Modular Landing
_Last updated: 2026-03-10_

---

## Current State

- **Task:** Testnet page content update and de-duplication
- **Phase:** Complete — two commits pushed this session
- **Progress:** `testnet.html` is now fully testnet-specific and design-system compliant

## What We Did

Pulled all content from the reference testnet page (`https://floors-testnet-landing.vercel.app/`) and applied it to `testnet.html` within the modular design system. Then identified and removed all content that was duplicated from `index.html` (the main marketing page), replaced with testnet-specific structure.

## Decisions Made

- **Keep protocol pillars on testnet page** — They serve as architecture orientation for new testnet participants, not just marketing. Kept as brief one-liner cards (no body `<p>` text).
- **Remove feature rows entirely** — The 5 alternating feature rows (Price Floor, Downside Protection, Zero Liquidations, Fee Capture, Reserve Growth) were verbatim duplicates of the main page. Removed HTML, CSS (~100 lines), and JS.
- **Add hook panel** — New "Mathematical Proof of Backing" section added between hero and pillars, using the `hook-panel` pattern from the design system. Testnet-specific entry point.
- **Benefits → Genesis Rewards cards** — Replaced 5 generic protocol benefit cards with 3 testnet participation cards: Genesis Distribution, Tiered Access, Governance Alpha.
- **Live leaderboard data** — Updated rankings to match reference page wallet data (floors.eth 142.5k, whale.eth 89.2k, defi_guru 64.1k, etc.).
- **"Join Phase One" CTA** — Added inside the Genesis Rewards / leaderboard section header per reference page.

## Code Changes

**Files modified:** `testnet.html` only

**Session commits:**
- `7186c65` — Content from reference: hero subtitle, pillar headlines, leaderboard data, benefits cards, Join Phase One CTA
- `1c058f5` — Structural de-duplication: removed feature rows, added hook panel, stripped pillar body text

**Testnet page structure after this session:**
```
NAV
HERO         — "Floor Only Goes Up" + Genesis Testnet Live badge
HOOK PANEL   — "Mathematical Proof of Backing" + Launch Testnet CTA
PILLARS      — 6 cards, label + one-liner headline only
DIVIDER      — "748 participants. 140,000 points distributed. Phase One is live."
LEADERBOARD  — Genesis Rewards stats + rankings + tasks
BENEFITS     — Genesis Distribution / Tiered Access / Governance Alpha
FAQ          — 6 flip-cards (hover to reveal answers)
CTA          — "Join Genesis Phase One" + email capture
FOOTER       — Protocol / Resources / Company / Social
```

## Open Questions

- [ ] Real CTA link destinations — all buttons still point to `#`
- [ ] Real leaderboard data — rankings and stats are currently hardcoded placeholders
- [ ] Tier Distribution values in leaderboard stats column still show `—` dashes
- [ ] Footer copyright and version string ("v1.4.2-ALPHA") — confirm if correct

## Known Issues / Caveats

- `testnet.html` has no mobile hamburger nav (nav links collapse at <800px with no replacement) — flagged as a design-system bug in `docs/design/design-system.html` section 04
- Many local-only untracked files remain (`docs/`, `emails/`, `assets/images/`, `assets/illustrations/`, `assets/logos/partners/`, some animation files) — not deployed, not in scope
- The Lottie hero animation references `HeroIntro.json` / `HeroLoop.json` which are listed as untracked — animations are currently placeholder/non-functional on testnet page until the files are finalised

## Next Steps

1. [ ] Add visual/animation content to testnet page (user deferred to a later session)
2. [ ] Wire real CTA links (dApp URL, dashboard URL) when available
3. [ ] Replace hardcoded leaderboard values with live or API-driven data
4. [ ] Confirm hero animation files for testnet — reuse main page `Hero.json` or a separate one
5. [ ] Decide whether the FAQ 6-card grid needs testnet-specific questions added/updated

## Files To Review On Resume

- `testnet.html` — current live testnet page
- `index.html` — canonical modular system reference (do not duplicate into testnet)
- `docs/design/design-system.html` — authoritative token/component/pattern reference

## Context Notes

- Static site, no build step
- Deploy: GitHub `master` → Vercel (`https://floors-finance-landing.vercel.app`)
- User constraint: preserve the modular design system at all times — no standalone redesigns
- User preference: only deploy files actively intended for the live site
- Latest pushed branch: `master` at commit `1c058f5`
