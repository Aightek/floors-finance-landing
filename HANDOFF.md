# HANDOFF - Floors Finance Modular Landing
_Last updated: 2026-03-10_

---

## Current State
- **Task:** Keep `testnet.html` aligned with the modular Floors design system
- **Phase:** Correction / design-system enforcement
- **Progress:** The off-system standalone redesign was reverted; `testnet.html` is back on the prior modular layout and animation structure

## What Happened
- A standalone testnet redesign was built and pushed, but it replaced the established modular design-system patterns
- User flagged that as incorrect because the repo must continue using the existing modular system
- `testnet.html` was restored from the previous design-system-based revision to undo the off-system layout change

## Latest Repo / Deploy State
- Latest pushed commit before correction: `4f9619d` (`Redesign genesis testnet landing page`)
- GitHub branch last pushed: `master`
- Current production alias: `https://floors-finance-landing.vercel.app`
- Local working tree currently includes:
  - `testnet.html` restored to the prior modular version
  - `HANDOFF.md` updated to reflect the correction

## Decisions Made
- **Do not replace the modular page shell** - future testnet work must be composed from the existing system's hero, cards, feature rows, leaderboard, newsletter, and footer patterns
- **Preserve the design system over reference-page mimicry** - external references can inform copy/content, but not a wholesale visual/system rewrite
- **Keep repo changes limited to intended live-site files** - untracked support files remain out of scope

## Code Changes
**Files modified locally:**
- `testnet.html`
  - restored to the prior design-system-based implementation
  - reintroduced the modular layout structure:
    - topbar
    - hero with Lottie
    - hook section
    - cards / benefits
    - feature rows
    - leaderboard
    - newsletter CTA
    - footer
- `HANDOFF.md`
  - rewritten to reflect the rollback and current design-system constraint

## Design-System References
- `docs/design/design-system.html`
  - authoritative source for tokens, buttons, navigation, cards, feature panels, leaderboard, CTA sections, footer, and quality rules
- `index.html`
  - live implementation of the modular system patterns used by the marketing site

## Known Issues / Caveats
- The previously pushed commit `4f9619d` is not design-system compliant and should be superseded by a corrective commit/push
- `testnet.html` still uses placeholder CTA links (`#`)
- The design-system version still contains hard-coded leaderboard values and placeholder footer/resource links
- PowerShell emits a profile execution-policy warning on nearly every shell command in this environment; noisy but non-blocking
- There are still many local-only untracked support files in `docs/`, `emails/`, `assets/images/`, `assets/illustrations/`, `assets/logos/partners/`, and some animation files

## Next Steps
1. Commit the restoration of `testnet.html` and the updated `HANDOFF.md`
2. Push the correction to `origin/master` so the off-system redesign is no longer the latest commit
3. If more testnet work is needed, make copy/content changes inside the existing modular structure rather than replacing it
4. Wire real destinations for CTA/footer links if canonical URLs are available

## Files To Review On Resume
- `testnet.html` - restored modular testnet page
- `docs/design/design-system.html` - design-system source of truth
- `index.html` - canonical live modular implementation
- `HANDOFF.md` - current correction state

## Context Notes
- Static site, no build step
- Deploy source is GitHub `master` to Vercel
- User preference: do not add or deploy files that are not actively intended for the live site
- User constraint: do not deviate from the modular design system
