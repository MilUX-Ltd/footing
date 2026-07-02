# Footing changelog

## 1.1.1, 2026-07-02

Clears the `footing-update` skill's structural audit caution now the repo's live: `github.com/MilUX-Ltd/footing` confirmed public, under the `MilUX-Ltd` organisation, and resolving correctly. `footing-setup`, `footing-update`, and the `cyber-essentials-ready` manifest URL all verified by direct fetch against the live repo.

## 1.1.0, 2026-07-01

Closes Step 4 of the original plan: a thin layer of universal business fundamentals, true regardless of sector, shipped in the repo rather than generated per install.

- New `Resources/Business/Cash Flow Basics.md`: what to track, a simple runway calculation, and the early warning signs worth watching. General business practice, not sector-specific, no pre-populated numbers.
- New `Resources/Business/Data Protection Basics.md`: a deliberately thin, plain-English UK GDPR orientation, the four lawful bases this pack's CRM already tracks, and when a DPIA is and isn't needed. Points to the `build-dpia` skill for anyone who needs the real thing rather than duplicating it. Checked against the ICO's April 2026 guidance update.
- The CRM convention, the third item from the plan's original four-item list, was already complete as part of Step 1 (`CRM/CRM Guide.md`) plus the worked-example pages restored today; no new content needed there.
- Kanban board basics, considered for this release, was cut from scope.

## 1.0.0, 2026-07-01

Initial public release. Footing is the general-business sibling of Foothold: the same installable Obsidian and Cowork second-brain pack, built for established businesses, charities, and small firms introducing AI into how they already operate, rather than early-stage defence-sector founders.

- **Template.** Full vault structure forked from Foothold and reworked: defence-specific folders emptied or restructured (`Intelligence/defence-landscape` became `Intelligence/sector-landscape`, built live per install rather than pre-populated; `CRM/organisations` rebuilt around client, supplier, partner, competitor, investor, and trade-body relationship types). All named defence content stripped. `Knowledge/rules.md` genericised. Guide files rewritten by hand for the new audience. `CRM/contacts/active contacts/Matt Odell.md` and `CRM/organisations/suppliers/MilUX.md` restored as the canonical worked-example contact and organisation pages, matching Foothold's own pattern (the initial Step 1 build stripped these entirely, leaving no worked example in either folder).
- **Banner.** `assets/footing-banner.svg` follows Foothold's own visual language: dark Deep Green background, ascending-steps mark, bold uppercase wordmark. Tagline: "Find your footing with AI".
- **Skills.** All 42 touched skills reworked from Foothold's copies: 34 `pm-skills` reforked with defence framing removed, 4 given a mechanical brand and path swap, 2 given a light content pass (`write-sow`, `humaniser`), and 2 given targeted rework (`add-organisation` regeneralised to the new organisation taxonomy, `foothold-update` forked to `footing-update` pointed at this repo). All 42 audited under `skill-safety-audit`: 41 pass clean, 1 (`footing-update`) passes with a structural caution recorded in the skill itself pending this repo going live.
- **New `footing-setup` skill.** The install and onboarding skill. Mirrors `foothold-setup`'s bootstrap, build, and schedule-update mechanics, with two differences: onboarding questions rewritten for an established-business audience rather than an early-stage founder, and a new sector question and research step. If answered, the skill runs a short live round of research at install time and writes a small set of reference pages, an overview and, where genuinely relevant, a framework or portal page, straight into the new vault's `Intelligence/sector-landscape/`. This content is generated per install, not shipped pre-populated in the repo, and is never touched by `/footing-update`.
- **README, docs, tools.** README rewritten for a general-business audience with the "get your footing" framing. `docs/architecture.md` authored fresh against Footing's actual current structure. `tools/vault-viewer/` carried over from Foothold unchanged in function, brand references swapped.
- **Deferred to a fast-follow.** The zip-based alternate install path (`installer/foothold-setup-from-zip` in Foothold) has no Footing equivalent yet. The primary GitHub-fetch install path ships first; the zip fallback is added if and when it's needed.
