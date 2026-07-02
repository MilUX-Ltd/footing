---
name: footing-setup
description: Install Footing — bootstrap the vault structure and run conversational onboarding. Fetches the latest template directly from the public Footing GitHub repo, creates folders at the user's chosen path, substitutes placeholders, interviews the user via seven sequential AskUserQuestion calls to personalise the canonical pages (including a sector question that triggers live sector-landscape research), and offers to schedule `/footing-update` on a weekly or monthly cadence. Use when the user says "set up Footing", "install Footing", "onboard me", or runs /footing-setup. Does NOT require terminal access.
audited: pending
audit_verdict: pending
audited_with: pending
origin: built
maintainer: MilUX
license: MIT
---

# Footing — Install and Onboarding (GitHub fetch)

USE WHEN the user runs `/footing-setup` or asks to install Footing, set up a new pack, or onboard themselves into a fresh Footing vault.

This skill fetches directly from the public GitHub repo at `MilUX-Ltd/footing`. It does not rely on the local plugin install's template directory, so installs are always against the latest published content.

Six-phase process:

- **Phase A: Bootstrap.** Silent. Resolve target path, fetch the template tree from GitHub, substitute placeholders, write files.
- **Phase B: Onboarding.** Seven sequential questions via AskUserQuestion, one per call.
- **Phase B+: Context drop.** One optional question inviting files, links, or folder paths to deepen personalisation.
- **Phase B2: Sector research.** Uses the sector answer from Phase B to research and write a small set of sector-landscape reference pages into the user's own vault, live at install time.
- **Phase B Build:** Populate the canonical pages from the corpus assembled across Phase B and Phase B+.
- **Phase C: Schedule updates.** One question offering to schedule `/footing-update` on a recurring cadence (weekly, monthly, or manual).
- **Phase D: Confirm completion.** Final summary, including the schedule the user opted into if any, and what sector-landscape pages were built.

## Pre-flight Check

Check if `CLAUDE.md` exists in the target directory (only at the exact target path — do NOT search subdirectories or parents).

- **If it exists.** The vault is already set up. Use AskUserQuestion:
  - Question: "This vault is already set up. What would you like to do?"
  - Option 1: `Re-run the interview` — Keep existing structure; refresh canonical pages from new answers.
  - Option 2: `Full reset` — Delete existing vault content and start fresh. (Confirm twice before proceeding.)
  - Option 3: `Cancel` — Do nothing.
- **If it does not exist.** Proceed with the full setup.

---

## Phase A: Bootstrap

Phase A is fully automated. No user input. Lay down the vault structure from the latest GitHub state, then move to Phase B.

### Step A.1: Resolve target directory

Default target: `~/Obsidian/{{pack_name}}/`. If `{{pack_name}}` is not yet set, default to `~/Obsidian/Footing/`.

If the target directory already contains files, verify with the user before continuing. Do not overwrite without consent.

### Step A.2: Fetch the latest file tree from GitHub

Call the GitHub tree API:

```
GET https://api.github.com/repos/MilUX-Ltd/footing/git/trees/main?recursive=1
```

Use the WebFetch tool. Public repo, no auth required.

Filter the response to entries where `type == "blob"` and `path` starts with `footing/template/`.

### Step A.3: Fetch and write the template

For each shipping file (collected in Step A.2):

1. Compute the corresponding target path. Strip the `footing/template/` prefix from the GitHub path.
2. Apply placeholder substitution to the filename (any `{{...}}` token gets replaced with the value the user provides in Phase B, or a sensible default).
3. Fetch the raw content from GitHub:

   ```
   GET https://raw.githubusercontent.com/MilUX-Ltd/footing/main/<full-path>
   ```

4. Apply placeholder substitution to the file content.
5. Create any missing parent directories at the target.
6. Write the file.

Order doesn't matter; the tree fetch gives you the full list in one call, then per-file fetches can run in parallel where convenient.

### Step A.4: Write `.footing/config.yml`

Create `.footing/config.yml` at the target root with the substitution values used **and** a baseline `last_known_shas:` map keyed by vault-relative path, set to the GitHub blob SHA each file came from in the tree fetch:

```yaml
footing:
  installed_at: <today's ISO date>
  version: <from footing/.claude-plugin/plugin.json at latest commit, if present>
  last_synced: <today's ISO date>
  pack_name: <value>
  pack_slug: <value>
  pack_owner: <value>
  pack_owner_email: <value>
  pack_owner_linkedin: <value or empty>
  pack_owner_phone: <value or empty>
  pack_org: <value>
  pack_org_slug: <value>
  pack_org_website: <value>
  sector: <value from Phase B Q2>

last_known_shas:
  Knowledge/rules.md: <sha from tree fetch>
  Knowledge/tagging-policy.md: <sha from tree fetch>
  # ...one entry per shipping file, keyed by post-substitution vault-relative path
```

The SHA map is the source of truth for the three-way reconcile in future `/footing-update` runs. It tells the update skill exactly which version each file is "at" when the user runs it, so the skill can distinguish between an unedited file the user is happy to overwrite and a file the user has personalised.

Sector-landscape pages built in Phase B2 are **not** tracked in `last_known_shas` — they are generated locally from live research, not fetched from the public repo, so they are the user's own content from the moment they're written. `footing-update` never touches them.

### Step A.5: Confirm bootstrap

Tell the user briefly:
- "Vault structure created at `<target path>`."
- List the top-level folders.
- "Now I'll ask seven quick questions to personalise the canonical pages, then offer you a chance to upload any extra files or links you want me to learn from."

Then move to Phase B.

---

## Phase B: Onboarding

Seven focused questions, asked **sequentially via AskUserQuestion** — one question per call, never batched.

For each question:
- Put the full prompt in the `question` field.
- Provide three quick-pick archetype `options` plus an explicit `Skip` option.
- "Other" is auto-added by the tool — that's where the user types long-form or pastes a link.
- Use the listed `header` (max 12 chars).
- Set `multiSelect: false`.
- After each answer, move to the next question. No commentary, no recap, no summarisation between questions.
- If the user picks `Skip` or leaves `Other` empty, treat the question as skipped and move on.

**Before Q1, send one short orienting message** (no AskUserQuestion yet):

> "Seven quick questions to personalise your vault, then I'll ask if you want to drop in extra files or links for deeper context. Each question has shortcut options — pick 'Other' to type or paste a link. Skip any you want. Reply 'skip all' to proceed with defaults."

If the user replies "skip all" at any point, stop asking and proceed to Phase B+. Note: Q2 (sector) has no safe default for Phase B2's research step, so if it's skipped, Phase B2 is skipped too rather than guessed at (see Phase B2).

This is an established business adopting AI for the first time, not a founder pitching from zero. Every question below is written for someone with a running operation, existing customers, and existing ways of working, not someone starting a venture from a blank page.

### Q1 — You. Header: `You`

- Question: "Quick intro. Your name, your role, and what you're known for in your line of work. What would you want a respected peer to say about you?"
- Options:
  - `Owner / operator` — "I run the business day to day"
  - `Senior leader` — "I run a function or team within it"
  - `Specialist / practitioner` — "I do the work, not the running of it"
  - `Skip` — "Skip this question"

Capture: name, role, professional background, peer-positioning quote.

### Q2 — Sector. Header: `Sector`

- Question: "What sector is your business in, and what's genuinely distinctive about it compared to other sectors? Think regulation, how customers buy, who the key bodies or standards are, what trips up outsiders. This shapes the reference content I build into your vault next."
- Options:
  - `Regulated sector` — "Healthcare, finance, professional services, and similar"
  - `Retail / consumer` — "Selling direct to consumers, physical or online"
  - `B2B services or trades` — "Selling to other businesses, or a skilled trade"
  - `Skip` — "Skip this question — build a generic vault with no sector research"

Capture: sector name, what's distinctive about it, any named bodies, standards, or regulations the user already mentions. This answer drives Phase B2; a real answer here (even a short one) is worth more than a rich answer to any other question, because it's the only input Phase B2 has to work from.

### Q3 — What you do, and who buys. Header: `Offer`

- Question: "What your business sells or delivers, the problem it solves, and who buys it (their role and the kind of organisation). A couple of real customer examples if you have them."
- Options:
  - `Product or platform` — "We sell a product or platform"
  - `Service or delivery` — "We sell expertise or delivery work"
  - `Retail or physical goods` — "We sell goods, direct or through retail"
  - `Skip` — "Skip this question"

Capture: offer, problem solved, customer archetype, named examples.

### Q4 — What sets you apart. Header: `Wedge`

- Question: "Why customers pick you over the alternative. Your point of view on your market, what you do differently, what you'd tell a new hire about the thing that actually wins business. In your words or theirs."
- Options:
  - `Clear differentiation` — "I know what makes us different"
  - `Strong POV / reputation` — "I'll describe our thinking or reputation"
  - `Still figuring it out` — "Keep this light for now"
  - `Skip` — "Skip this question"

Capture: wedge, POV, key messages.

### Q5 — Voice. Header: `Voice`

- Question: "How you sound. A few descriptors (direct, warm, dry, technical, pragmatic), signature phrases you use, words you'd never use. Or paste a writing sample or a LinkedIn post URL and I'll extract."
- Options:
  - `Paste writing sample / URL` — "Pull voice from my actual writing"
  - `Describe my voice` — "I'll describe it in 'Other'"
  - `Use sensible defaults` — "Pick a reasonable voice for now"
  - `Skip` — "Skip this question"

Capture: voice descriptors, signature phrases, words-to-avoid.

### Q6 — Current priorities. Header: `Now`

- Question: "What's on your plate this quarter. Top 1–3 priorities (with a number if measurable), the active initiatives you're running, and any named clients, suppliers, or partners you're currently engaged with."
- Options:
  - `Revenue / growth focus` — "Money is the main metric"
  - `Build / ship something` — "Building, launching, or improving something"
  - `Relationships / delivery focus` — "Keeping existing clients or partners right"
  - `Skip` — "Skip this question"

Capture: priorities, named initiatives, named engagements.

### Q7 — Stack and drains. Header: `Stack`

- Question: "The tools you actually use (CRM, comms, AI, file storage, calendar, knowledge), any AI agents already wired into your work, plus the 1–2 things draining your attention or workflows you'd kill to automate."
- Options:
  - `Walk through stack + drains` — "I'll describe in 'Other'"
  - `Mostly attention drains` — "Focus on what's draining me"
  - `Mostly tooling questions` — "I want help thinking through tools"
  - `Skip` — "Skip this question"

Capture: tool stack, agents already wired, drains, automation candidates.

---

## Phase B+: Context drop

After Q7 (or "skip all"), call one final `AskUserQuestion` to invite extra source material.

- Question: "Anything else I should pull from before building? Upload files (PDFs, MDs, DOCXs), paste links (LinkedIn, websites, Notion pages, Google Docs), point me at a local folder, or paste raw text. The more I have, the more personalised your vault will be."
- Header: `Context`
- Options:
  - `Yes — I'll paste links / upload files` — "Walk me through it"
  - `Yes — point me at a folder on disk` — "I have local files"
  - `No — use just the answers above` — "Build with what we have"
  - `Skip` — "Skip this step"

**If the user picks a "Yes" option** (or pastes content directly):

1. Collect everything they share. Be greedy.
2. For each link: call WebFetch (or WebSearch if the URL is a search). Extract relevant content.
3. For each uploaded file or local file path: read directly with Read (or Bash with pandoc for docx/pptx).
4. For a local folder path: use Glob to enumerate, then read each file.
5. Maintain a context corpus in working memory — every fact, name, number, quote, URL. Tag each by likely target page.
6. After ingestion, briefly tell the user what you pulled. One sentence. Then proceed to Phase B2.

**If the user picks `No` or `Skip`**: proceed straight to Phase B2 with only the Q1–Q7 answers.

---

## Phase B2: Sector research

This is the step Foothold doesn't have. Foothold ships with defence-sector reference content pre-populated in the public repo, because it only ever serves one sector. Footing serves any sector, so it can't pre-populate anything useful in the public repo; instead it researches and writes a small set of sector-landscape pages **live, into the user's own vault, at install time**, using Q2's answer as the brief. These pages are never written back to the public Footing repo — they're the user's own content from the moment they're created.

**Skip this phase entirely if Q2 was skipped or gave no usable sector information.** Do not guess a sector or research a generic placeholder; tell the user in Phase D that sector-landscape pages weren't built because the sector question was skipped, and that they can ask for this later.

### What to produce

A small, structured set: **3 to 5 pages**, built from real web research (WebSearch / WebFetch), each citing its sources, written into `Intelligence/sector-landscape/` (the folder structure from Step 1 ships with empty `Portals/`, `Programmes/`, `Frameworks/` subfolders plus the root of `sector-landscape/` itself):

1. **`Intelligence/sector-landscape/<Sector> Landscape.md`** (always produced if Phase B2 runs). One overview page: what's distinctive about the sector per Q2's answer, the regulatory or compliance environment if one exists, how buying typically works, the 2-4 bodies or standards that matter most, and a short "what trips up outsiders" section if the research surfaces one. This is the single highest-value page; if research time is short, this is the one to prioritise.
2. **`Intelligence/sector-landscape/Frameworks/<Name>.md`**, one page per genuinely relevant standard, certification, or compliance framework common in the sector (for example, a quality or data standard, a professional accreditation, a sector-specific compliance regime). Produce 1 to 2 of these if the sector has clear examples; produce none if it doesn't rather than inventing generic filler.
3. **`Intelligence/sector-landscape/Portals/<Name>.md`**, one page for a genuinely useful public portal, directory, or regulator site relevant to the sector, if one exists (for example a regulator's public register, an industry body's member directory). Produce 0 to 1 of these.
4. **`Intelligence/sector-landscape/Programmes/`** — leave empty unless the sector has an obvious equivalent to a funding programme or major public initiative (a grant scheme, a sector-specific government programme). Most sectors won't; don't force a page into this subfolder just to fill it.

Total should land at 3 to 5 pages including the overview. If the sector is narrow or research turns up little, 3 (overview plus one or two frameworks) is a fine outcome; don't pad with weak pages to hit a number.

### How to research

- Use WebSearch and WebFetch. Public, searchable sources only — the same rule Foothold's own content layer uses: if it lives in a publicly searchable place, it's fair to cite; if it would need a relationship or private access, leave it out.
- Cite every factual claim with a source link in the page body, in a short "Source material" section, matching the pattern the vault's own `add-organisation` skill uses.
- Keep it fast. This is a live install-time step, not an open-ended research project. Budget for a handful of searches per page, not an exhaustive literature review. The user is waiting.
- Use the frontmatter shape already established for `Intelligence/` pages in the vault: `type: reference` (or the matching type already used by the folder's Guide), plus whatever fields `Intelligence/sector-landscape/Intelligence Guide.md` (renamed from Foothold's Intelligence Guide during Step 1) specifies.
- Write in the vault's established style: British English, no em dashes, plain and factual.

### Tell the user what happened

Before moving to Build, one short line: "Built N sector-landscape pages on [sector] from public sources — you'll find them in Intelligence/sector-landscape/." If Phase B2 was skipped, say that instead, briefly.

---

## Phase B Build: Populate canonical pages

Build everything you can from the Q answers and the context corpus. Work silently. Don't narrate each file.

### Critical rule: scaffolds, not outputs

The templated stubs you wrote in Phase A are **scaffolds** showing the section structure. They are **not** the output. Do not commit a page with bracketed placeholders or italicised hint text intact.

For every file you populate:

1. **Read the existing templated stub** to learn the section structure.
2. **Replace every placeholder** (`{{...}}`, `[bracketed text]`, *italicised hint text*) with real data from Q1–Q7 + the context corpus.
3. **If a section has zero supporting data** after exhausting both Q answers and the corpus: **omit the entire section**. Never leave placeholders behind.
4. **If only some items in a section have data**: keep the section, drop the empty items.
5. **Use the user's actual words, names, numbers, URLs, and quotes** wherever the corpus has them. Preserve specificity.
6. **Cross-reference**: a single fact may belong in multiple files. Place it everywhere it's relevant.
7. **Frontmatter `last_reviewed:`** = today's date.

A finished canonical page should read like a human-written document about the user's business. If it reads like a fillable form, go back and fill it.

### Pages to populate

For each file below, populate from Q answers + corpus. Skip files where there is no supporting data.

| File | Sources | Frontmatter to set |
|------|---------|--------------------|
| `Context/<pack_owner>.md` | Q1 (name, role, background), Q2 (sector), Q3 (offer, customer), Q4 (POV), Q7 (drains) + corpus | `name`, `role`, `email`, `linkedin`, `created` |
| `Context/Brand.md` | Q4 (positioning), Q5 (voice, voice descriptors, signature phrases, words to avoid) + corpus | `last_reviewed` |
| `Context/Strategy.md` | Q6 (priorities, initiatives, engagements) + corpus | `last_reviewed` |
| `Context/Team.md` | Q1 + corpus (if user mentions a team) | `last_reviewed` |
| `Context/Stakeholders.md` | Corpus (only if user has named external stakeholders) | `last_reviewed` |
| `Operations/email-signature.md` | Q1 (name, role), Q3 (org), corpus | none |

### Initial Daily note

Create `Daily/<YYYY-MM-DD>.md` (today's date):

```markdown
---
type: daily-note
date: YYYY-MM-DD
---
# YYYY-MM-DD

## Footing installed

Footing pack set up today. Onboarding complete: canonical pages drafted from the install interview, sector-landscape pages built from live research (if Q2 was answered).

### Next steps

- Open this folder in Obsidian.
- Review the Guide pages in each folder to understand the conventions.
- Use the per-folder skills as you add content.
```

---

## Phase C: Offer scheduled updates

Footing gets new skills and structural improvements added over time. The user can either remember to run `/footing-update` themselves, or have it scheduled to run automatically. Offer the choice.

Use AskUserQuestion with **one** question:

- Header: `Schedule`
- Question: "Footing gets new skills and structural improvements over time. Want me to schedule `/footing-update` to run automatically so your pack stays current?"
- Options:
  - `Weekly` — "Run every Monday morning"
  - `Monthly` — "Run on the 1st of each month"
  - `Custom cadence` — "I'll tell you when in 'Other'"
  - `No, I'll run it manually` — "I'll trigger updates myself"
- `multiSelect: false`

### Acting on the answer

- **Weekly**: call `mcp__scheduled-tasks__create_scheduled_task` with cron expression `0 9 * * 1` (every Monday at 09:00) and prompt `Run /footing-update to pull the latest content from the Footing repository into the vault at <vault path>. Apply the three-way reconcile per the SKILL.md; surface any conflicts to the user.`
- **Monthly**: same as weekly but cron `0 9 1 * *` (1st of the month at 09:00).
- **Custom cadence**: read what the user typed in `Other`. If it parses to a clear cadence (e.g. "every Wednesday at 7am", "twice a month", "every two weeks"), construct the matching cron expression and create the task. If it's ambiguous, ask one clarifying question, then create. If still ambiguous, default to weekly and tell the user.
- **No, I'll run it manually**: do not create a scheduled task. Briefly remind the user they can re-run `/footing-setup` later (or ask Cowork directly) to set up a schedule down the line.

### Offer the monthly sector scan

The sector reference pages in `Intelligence/sector-landscape/` were researched live during this install, against the sector and area the user named in the interview. They decay from today unless refreshed. Offer the refresh as a second scheduling question, via AskUserQuestion:

- Header: `Sector scan`
- Question: "Your sector pages were researched today and will age. Want me to schedule `/sector-scan` to re-run that research monthly and tell you what changed?"
- Options:
  - `Monthly` — "Run on the 2nd of each month"
  - `No thanks` — "I'll run /sector-scan myself when I want a refresh"
- `multiSelect: false`

Acting on the answer:

- **Monthly**: call `mcp__scheduled-tasks__create_scheduled_task` with cron `0 9 2 * *` (2nd of each month at 09:00, offset from footing-update on the 1st) and prompt `Run /sector-scan against the vault at <vault path>. Read the sector definition from .footing/config.yml and the Context pages, refresh Intelligence/sector-landscape/, and write a dated scan note summarising what changed. Vault writes only; nothing external.`
- **No thanks**: no task. Mention the skill exists whenever they want a refresh.

Record the choice under a `sector_scan:` key in the `schedule:` section of `.footing/config.yml`, same shape as the update schedule.

### Offer the daily brief

The pack ships a `daily-brief` skill that writes each day's note as a generated brief (engagements, initiatives, rolled-forward items, upcoming events) rather than a form the user fills in. Offer it via AskUserQuestion:

- Header: `Daily brief`
- Question: "Want your daily note written for you each weekday morning? `/daily-brief` reads what you're working on and has the day's brief waiting before you are."
- Options:
  - `Weekday mornings` — "Run at 08:00, Monday to Friday"
  - `No thanks` — "I'll run /daily-brief myself when I want one"
- `multiSelect: false`

Acting on the answer:

- **Weekday mornings**: call `mcp__scheduled-tasks__create_scheduled_task` with cron `0 8 * * 1-5` and prompt `Run /daily-brief against the vault at <vault path>. Write the Daily Brief section into today's note per the SKILL.md. Vault writes only; nothing external.`
- **No thanks**: no task. The first-week guide's Day 3 introduces the skill anyway.

Record the choice under a `daily_brief:` key in the `schedule:` section of `.footing/config.yml`, same shape as the update schedule.

### Offer the first-week check-in

The template ships with `Getting Started - Your First Week.md` at the vault root, and Home.md points at it. After the scheduling questions, offer one more thing (a plain question in conversation is fine; no AskUserQuestion needed): "Want me to check in with you in a week to see how the first-week list is going?"

- **Yes**: call `mcp__scheduled-tasks__create_scheduled_task` with a one-off `fireAt` seven days from today at 09:00 and prompt `Open <vault path>/Getting Started - Your First Week.md, see which items are ticked, and ask the user how the first week went. Help with whichever unticked item they want to tackle next. This is a one-off check-in, not a recurring task.`
- **No**: point out the guide's own first line tells them how to ask for a reminder later.

Either way, close Phase C by telling the user their first move is the guide's Day 1: read their two Context pages.

### Record the choice in `.footing/config.yml`

Whatever the user picks, append a `schedule:` section to `.footing/config.yml` so the choice is auditable and can be re-asked on re-run:

```yaml
schedule:
  cadence: weekly | monthly | custom | manual
  cron: "<cron expression>" or null if manual
  task_id: "<scheduled-tasks task id>" or null if manual
  set_on: <today's ISO date>
```

If the user later wants to change the cadence (or remove the schedule), they can ask Cowork to update or cancel the scheduled task by ID, or re-run `/footing-setup` which will see the existing schedule and offer to amend it.

---

## Phase D: Confirm completion

Tell the user:

- A one-line summary of what was created.
- What sector-landscape pages were built (or, if Q2 was skipped, that none were and how to get them later).
- "Open this folder in Obsidian to see your vault."
- If they opted into a scheduled update: "I've scheduled `/footing-update` to run <cadence — e.g. every Monday at 9 AM>. You'll get a notification each time it runs and can review any conflicts before they're applied."
- If they declined: "If you want to pull new content from Footing later, just run `/footing-update` here in Cowork. No need to reinstall anything."
- Suggest one concrete next action based on the user's Q answers.

---

## Guidelines

- Always fetch from GitHub, never from the local plugin install's template directory. The plugin only delivers the skills; GitHub is the source of truth for content.
- Phase A is fully silent. No user input.
- Phase B is exactly seven questions, asked one at a time via AskUserQuestion. No follow-ups inside a question. No batching.
- Phase B+ is one final AskUserQuestion offering files / links / folders. Always ask, even if Q1–Q7 looked rich.
- Phase B2 runs only if Q2 (sector) got a real answer. It writes into the user's own vault, never back to the public repo, and stays fast — a handful of searches per page, not an open-ended research project.
- For every link the user pastes, fetch it (WebFetch / WebSearch). For every file or folder, read it (Read / Glob). Merge into a single corpus before building.
- Templates are scaffolds, never outputs. Replace every placeholder. If a section has no data after exhausting answers + corpus, omit it.
- Preserve specificity. Use the user's exact names, numbers, URLs, and phrasing.
- Only create canonical pages that have real content. Don't populate empty templates.
- Don't narrate file-by-file. Build silently. Summarise at the end.
