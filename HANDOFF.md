# HANDOFF - Floors Finance Modular Landing
_Last updated: 2026-03-10_

---

## Current State
- **Task:** Redesign `testnet.html` into a standalone Genesis Testnet release page while keeping repo/deploy changes limited to intentionally shipped live-site files
- **Phase:** Implementation
- **Progress:** New local `testnet.html` redesign is complete in code, received a structural/accessibility QA pass, but has not been visually browser-QA'd, pushed, or deployed

## What We Did
- Fetched and reviewed the reference page at `https://floors-testnet-landing.vercel.app/`
- Replaced the old `testnet.html` that duplicated the main landing-page structure with a new standalone testnet page
- Kept the leaderboard/tasks content from the previous `testnet.html`, but removed the duplicated landing-page hero imagery, Lottie usage, feature rows, benefits grid, and old CTA/email capture pattern
- Added a follow-up polish pass on the new page to improve semantics and interaction quality without adding new deploy surface area

## Latest Repo / Deploy State
- Latest pushed commit: `17edca1` (`Reorganize live site assets`)
- GitHub branch last pushed: `master`
- Current production alias: `https://floors-finance-landing.vercel.app`
- Current production deploy still reflects the pre-redesign `testnet.html`
- Local working tree includes uncommitted changes to `testnet.html` and `HANDOFF.md`

## Decisions Made
- **Use the reference page's content model for testnet** - the testnet page should explain the release and point system, not mirror the main marketing landing page
- **Remove all image/animation dependencies from `testnet.html`** - the new testnet page is intentionally lighter and no longer depends on Lottie, hero animations, or landing-page visual duplication
- **Keep the existing leaderboard section content** - wallet rankings and point-earning tasks from the prior `testnet.html` remain useful and were preserved in the redesign
- **Do not deploy yet** - user requested a design-focused pass first; no GitHub/Vercel update was done for this redesign

## Code Changes
**Files modified locally:**
- `testnet.html`
  - replaced the old duplicated page structure with a new standalone testnet release page
  - updated copy direction to match the reference page:
    - `Genesis Testnet Live`
    - `Floor Only Goes Up`
    - `Mathematical Proof of Backing`
    - `Protocol Pillars`
    - `Genesis Rewards`
    - `Common Questions`
  - removed:
    - hero Lottie setup
    - feature-row animation system
    - duplicated benefits/product card sections
    - old flip-card FAQ
    - inline email capture CTA module
    - logo/image asset dependency in the page itself
  - kept:
    - leaderboard stats
    - top wallets list
    - point-earning task list
  - replaced interactive behavior with a small FAQ accordion script only
  - follow-up polish pass:
    - added skip link and `main` landmark
    - added visible keyboard focus styles
    - upgraded FAQ accordion with `aria-controls` and `hidden` state sync
    - changed `Top wallets - Feb 14, 2026` to a neutral `Leaderboard snapshot` label to avoid a stale hard-coded date
- `HANDOFF.md`
  - updated to reflect the current redesign state

## Reference Content Used
- Source page reviewed: `https://floors-testnet-landing.vercel.app/`
- Core copy patterns brought into the redesign:
  - `Genesis Testnet Live`
  - `Floor Only Goes Up`
  - `Next-generation autonomous liquidity protocol providing deterministic floor price guarantees and interest-free credit.`
  - `Mathematical Proof of Backing`
  - `Every protocol operation reinforces the Reserve Pool, programmatically raising the floor price without external dependency.`
  - `Protocol Pillars`
  - `Genesis Rewards`
  - `Participate in the Testnet ecosystem to earn weighted points clusters.`
  - `Genesis Distribution`
  - `Tiered Access`
  - `Governance Alpha`
  - `What defines a "Floor Price"?`
  - `Is there liquidation risk?`

## Known Issues / Caveats
- No browser QA has been run on the redesigned `testnet.html`; the latest pass was code-level QA only
- The new `testnet.html` is local only and not yet pushed or deployed
- CTA links are still placeholders (`#`)
- PowerShell emits a profile execution-policy warning on nearly every shell command in this environment; noisy but non-blocking
- There are still many local-only untracked support files in `docs/`, `emails/`, `assets/images/`, `assets/illustrations/`, `assets/logos/partners/`, and some unused animation files

## Next Steps
1. Open and visually QA local `testnet.html`
2. Tighten layout/copy if needed after QA against the reference page
3. Wire real destinations for the testnet CTA links if available
4. If approved, commit only `testnet.html` and deploy the redesign to GitHub/Vercel
5. Optionally decide whether to keep or ignore the local-only support files

## Files To Review On Resume
- `testnet.html` - redesigned standalone Genesis Testnet release page
- `index.html` - unchanged live main landing page
- `HANDOFF.md` - current session state
- `vercel.json` - static no-build deploy configuration

## Context Notes
- Static site, no build step
- Deploy source is GitHub `master` to Vercel
- User preference remains: do not add or deploy files that are not actively intended for the live site
- Current production site has **not** received the new `testnet.html` yet
