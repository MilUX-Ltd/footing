# Footing changelog

## 2.0.0, 2026-07-02

The onboarding release, matching Foothold 2.0.0 and a major version for the same reason: it changes what installing Footing feels like.

- **The small-firm questions answered.** New `Resources/Ways of Working/Where Your Data Lives.md`: what stays local, what Claude sees and under whose terms, what never goes in (caveated client material, sensitive personal data without a basis, regulated records), how the setup sits alongside Cyber Essentials, and what to say to a client's security questionnaire. The README gains a matching section, and its team section is rewritten as "Running Footing in a small firm": a month-by-month adoption path, the curator as a delegable role, honest per-seat maths, and a "what to bring, what to leave" rule.
- **README rewritten around outcomes, in plain English.** The jargon-first opening replaced with a plain-terms explanation of what the system is, a "what changes in your first 30 days" section, the Copilot objection answered, an honest cost-and-effort table, a "Yours, forever" ownership clause, a maintainer provenance paragraph, and the Vault Viewer promoted to the try-before-you-install path.
- **Onboarding is now a guided brain dump.** `footing-setup` Phase B replaces seven sequential questions with two rich forms (seven categories, same substance): per category a brain-dump box, a links-and-paths field, and file upload, with dictation transcripts explicitly recommended as the highest-yield input. The sector category keeps its special weight, as the brief for the install-time sector research, and the orienting message says so. Falls back to the question flow where the form surface isn't available.
- **Re-running setup is now discovery-first.** The re-run flow reads config (including the recorded sector) and Context silently, presents a "discovered from your vault" summary, and asks only "what's changed, or what did I get wrong?", offering a Phase B2 re-run if the sector definition moved.
- **Probe, don't ask.** `import-relationships` detects and read-only-probes CRM connectors before asking anything, reporting exact errors with a skip-or-fix choice; `daily-brief` does the same for the calendar, and reports a failing connector once rather than daily.
- **The first-week check-in became a personalisation loop.** "A week in — what feels wrong, missing, or harder than it should be? I'll change it." Smallest change, confirm, ask what else, and park unreached wants in `Ideas/` for the next session.
- **The audience broadened, formally.** The README no longer excludes early-stage founders; Footing is for anyone putting AI to work, and setup now opens with one fork question ("running something established, or starting something new?") that shapes build emphasis and the Day 2 recommendation without gating anything. The empty investor A-Z subfolders are gone from the shipped structure (letter-splitting stays in the Guides as advice for when a set grows); `investors/` itself remains, since founders raise and charities have funders.
- **Setup now creates the structural folders explicitly** (Step A.3b, canonical list in the skill). Git carries no empty directories, so the tree fetch alone never could; this closes the gap where a fresh install arrived without `Customer Engagements/`, the CRM buckets, or the sector-landscape subfolders Phase B2 writes into.
- **New `Skills/ops-skills/` category, four skills.** The established wing gets tooling to match the founder wing's pm-skills. `process-map`: one process per run out of the owner's head onto a page, with a Mermaid map, honest pain points, and automation candidates split from keep-human steps. `sop-capture`: turns a mapped process into a procedure a competent newcomer could follow cold, and notes that a good SOP is most of a skill specification. `service-blueprint`: a proper UCD method for seeing a service the way the customer lives it, moments of truth and failure points marked. `ai-readiness`: a four-lens self-assessment (data, processes, people, governance) with one first move per lens and no scores, benchmarks, or promises; organisations wanting a professional assessment are pointed, once and plainly, at MilUX's Fit-for-Purpose Assessment. The setup fork's completion summary now names process-map and ai-readiness for the established wing. All MIT licensed, MilUX originals.
- **New `Skills/meta-skills/curator/`: the budgeted curation sweep.** Fixes mechanical defects with exactly one right answer (broken wikilinks with an unambiguous target, missing frontmatter derivable from the folder Guide, unescaped pipes in table wikilinks) within hard per-run caps: 200 reads, 20 fixes, 30 report items, folder rotation for larger vaults. Everything needing judgement goes to a dated Curation Report instead of being touched; no renames, no archiving, no deletion, ever. Setup offers a monthly schedule (3rd of the month, after footing-update on the 1st and sector-scan on the 2nd). The skill curates hygiene, not knowledge; meaning stays with the owner. MIT licensed, MilUX original.

## 1.5.0, 2026-07-02

- New `How to Use This Vault.md` at the vault root: the four working habits that make the system compound. Brief Claude like an intern in its first week (it never forgets a good briefing, because the briefing lives in the vault); describe your processes, because a process you can describe is a process you can automate; watch for repeatable patterns worth turning into a skill or a schedule, and tell Claude to watch too; and review both the work (self-review against the brief before anything is called done) and the working (regular retrospectives whose output is always a permanent change: a rule, an amended skill, a corrected Context page). Home.md and the first-week guide both link to it.

## 1.4.0, 2026-07-02

Kills the write-three-lines daily-note ritual shipped earlier today in 1.3.0. Asking the user to report what happened yesterday is a scrum anti-pattern; the vault already knows.

- New `Skills/meta-skills/daily-brief/`: writes the day's note as a brief FOR the user, generated from engagements, initiatives, items rolled forward from previous notes, upcoming events, and (where a calendar connector exists) today's meetings. Owns a `## Daily Brief` section per the Daily Guide convention and never touches the user's own writing. Hard cap of seven needs-attention items; a quiet day gets a short brief, honestly. MIT licensed, MilUX original.
- `footing-setup` Phase C now offers to schedule `/daily-brief` for weekday mornings at 08:00.
- `Getting Started - Your First Week.md` Day 3 rewritten: run the brief, schedule it if it earns its place. The standup ritual is gone.
- `Daily Guide.md` updated: the note can be created by the brief each morning; the user writes everywhere else.

## 1.3.0, 2026-07-02

The first-week and living-intelligence release.

- New `Getting Started - Your First Week.md` at the vault root: one small win a day (foundations, bringing existing relationships in, the daily-note habit, design system, sector pages), then week two onwards. Home.md now leads with it.
- New `Skills/meta-skills/sector-scan/`: re-runs the install-time sector research against the sector the user chose at setup, updates `Intelligence/sector-landscape/` respecting the user's own edits, and writes a dated what-changed note. A quiet month is reported in two lines, not padded. MIT licensed, MilUX original.
- `footing-setup` Phase C now offers to schedule `/sector-scan` monthly (2nd of the month, offset from footing-update on the 1st), and separately offers a one-off first-week check-in seven days after install. The sector chosen once at install becomes the standing search brief.
- `Home.md` rewritten: the Dataview query suggestions are now live query blocks (engagements, initiatives, recent contacts, latest published), with a one-line pointer to installing the free Dataview plugin.
- New `Resources/Ways of Working/Sync and Backup.md`: Obsidian Sync, git, iCloud, OneDrive/Dropbox/Google Drive and Syncthing compared honestly, including the iOS limitation on generic cloud drives, plus the sync-is-not-backup discipline.

## 1.2.0, 2026-07-02

The CRM bootstrap release. Footing's audience arrives with years of existing relationships; until now the only way in was one contact at a time.

- New `Skills/crm-skills/import-relationships/`: seeds the vault CRM from wherever the relationships currently live. Connector-first (if the user's CRM has an MCP connector in Cowork, connect and read directly), CSV export as the second path (HubSpot's column set mapped without ceremony, any other CRM's export treated as a mapping to confirm), and a guided interview as the floor. Triage before import is the heart of it: active relationships get full pages, reference contacts get reference pages, and stale records stay behind, because importing two thousand dead contacts creates a vault nobody trusts. Preview gate before any batch write, lawful-basis tagging per the CRM convention, never edits or deletes existing pages. MIT licensed, MilUX original.

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
