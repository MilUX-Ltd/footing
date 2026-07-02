<p align="center">
  <img src="assets/footing-banner.svg" alt="Footing" width="720">
</p>

# Footing

"Get your footing" is the moment you stop slipping and stand on solid ground. Whether you're an established business bringing AI into how you already operate or a founder starting something new, that's the hard part. Not the tools themselves, but knowing where to plant your feet: what to hand over, what to keep to yourself, and how to set the whole thing up so it still makes sense in six months.

Footing gives you that solid ground in an evening.

Footing is a ready-made **knowledge system for your business**: a set of organised, private files that live on your own computer, plus an AI assistant that reads and maintains them for you. In plain terms: everything about your business (your customers, your priorities, how you work, what's happening in your sector) captured once, in one place, so that the AI helping you actually knows your business rather than starting from scratch every conversation.

It runs on two applications: **Obsidian**, a free app for working with linked notes (think of it as a filing cabinet that shows you the connections), and **Claude**, the AI assistant, through its desktop app. Footing installs with one command, interviews you about your business, researches your specific sector, and hands you a working system the same evening.

The operations still have to be run. Footing is the ground you run them from.

## What changes in your first 30 days

**Day 1.** The system knows your business: what you sell, who buys it, what sets you apart, what is on your plate this quarter. Getting that in takes about an hour of guided conversation. It has also researched your sector and written you a short set of reference pages covering the regulation and bodies that matter, and what trips up outsiders.

**Day 15.** Your day starts with a briefing written for you: what needs attention, what has stalled, who has gone quiet. Before a meeting, one command briefs you from your own relationship history; no more opening the call with "remind me where we got to". Your existing contacts are in, imported from whatever you use now, with the dead wood left behind.

**Day 30.** Written drafts are starting to sound like you, because the system holds real samples of your writing. The process that eats most of your week is mapped, with an honest answer about which parts a machine could take. Your sector pages have refreshed themselves.

If you want to see one before installing anything, the [Vault Viewer](tools/vault-viewer/) reads a Footing knowledge base in your web browser. No install, no account.

## What you get

- Reference pages researched for your sector at setup and written into your own files, not generic content shipped to everyone.
- Your contacts imported from whatever CRM or spreadsheet holds them now, triaged so only living relationships come in, then meeting prep that draws on them.
- A daily brief written for you each morning, process mapping that finds what is worth automating, procedures captured so they survive handover, and an AI-readiness self-assessment with no scores and no sales pitch.
- Guided onboarding, a first-week guide, and a short page on the working habits that make the system improve with use.
- One update command that pulls improvements from this repository without overwriting your own content.

## Isn't Copilot enough?

Fair question, since you may be paying for it already. Copilot works on the document or email in front of it and remembers nothing about your business between sessions. That puts the burden of context on you, every time. Footing keeps the context in your files: your strategy, your customers, your sector, the state of every piece of work. Every conversation starts from there, and knowledge captured this way stays when people leave. The two work fine side by side; they do different jobs.

## Audience

Owners, operators, and senior leaders at established businesses, charities, and small firms introducing AI into how they already work, and founders starting something new who want solid ground under it from day one. Setup asks which you are and shapes the system accordingly. No prior experience of Obsidian, Claude, or anything like them is assumed. Free and available to all. Hands-on onboarding and ongoing support are available from MilUX as a paid service; email for current pricing.

## Getting started

This is the install walkthrough. The whole thing takes about ten to fifteen minutes once you have Cowork and Obsidian open.

### What you'll need

- **A paid Claude subscription, with Cowork.** Cowork is Anthropic's desktop app for non-developers, and it runs inside a paid Claude plan. Sign up and subscribe at [claude.com](https://claude.com), then download the Claude desktop app; Cowork is a tab inside it. There is a running cost here: budget for one Claude subscription per person who will run the vault.
- **Obsidian.** Free knowledge management app. Download from [obsidian.md](https://obsidian.md). Obsidian Sync, used for keeping a vault in step across devices or people, is a paid add-on; a free alternative is covered under Scaling across a team below.

### Prefer a different stack?

Claude and Obsidian are the pairing we build for, and the one this walkthrough assumes. The pack itself is plain text, though, so it can be configured differently: open-source tools such as OpenCowork in place of Cowork, models you already run (including self-hosted ones), and whichever sync arrangement your setup needs. That is bespoke work rather than a walkthrough, and MilUX does it as a service. If you want the pack set up your way, email matt@milux.co.uk.

### What it costs, honestly

| Item | Cost | Ongoing effort |
|------|------|----------------|
| Footing itself | Free, MIT licensed | — |
| Claude subscription (with Cowork) | Your Claude plan, per person ([claude.com](https://claude.com) has current pricing) | — |
| Obsidian | Free | — |
| Obsidian Sync (optional, for multi-device) | Paid add-on; free alternative documented in the pack | — |
| Keeping the system honest | — | Plan for about half an hour a week of review and correction, less as it learns |
| Hands-on onboarding from MilUX (optional) | Paid; email matt@milux.co.uk for current pricing | — |

The half-hour a week is the real cost. It is also how the system learns your business: the corrections you make are the teaching.

### Step 1 — Run the setup

Open a new Cowork chat and paste the following:

```
Fetch https://raw.githubusercontent.com/MilUX-Ltd/footing/main/footing/skills/footing-setup/SKILL.md and follow the instructions in it exactly.
```

The skill takes over from here. It will:

1. **Ask one question first**: are you running something established, or starting something new? The answer shapes emphasis throughout; nothing is gated either way.
2. **Lay down your vault.** Create a folder structure at `~/Obsidian/Footing/` (or a custom path if you specify one). Silent step, takes a few seconds.
3. **Run a guided brain dump.** Two short forms covering seven areas: who you are, your sector, what you do and who buys it, what sets you apart, your voice, your current priorities, and your tool stack. Type, paste links, or upload documents against any of them; the single best input is a dictation transcript, rambled and untidied. The sector answer matters most, because it drives the next step.
4. **Research your sector.** The skill runs a short, live round of research and writes a small set of reference pages, an overview and, where genuinely relevant, a framework or portal page, straight into your own vault. Generated fresh for you at install time, not pulled from a shared library.
5. **Offer a context drop.** One further question inviting you to paste links, upload files, or point at a local folder of source material. The more you give it, the more personalised your vault will be.
6. **Build your canonical pages.** Silently. The skill drafts your operator profile, brand and strategy pages, email signature, and voice notes from the answers and corpus.
7. **Offer the running rhythm.** Whether to schedule `/footing-update` (weekly or monthly), a monthly refresh of your sector pages, a daily brief on weekday mornings, a monthly curation sweep, and a one-week check-in. Everything is optional and can be cancelled later.

When the skill finishes, it tells you where the vault was created, what sector-landscape pages (if any) it built, and which schedule (if any) is now in place.

### Step 2 — Open your vault in Obsidian

1. Launch Obsidian.
2. Click "Open folder as vault".
3. Point at your new Footing vault folder (default: `~/Obsidian/Footing/`).
4. Click "Open".

Your vault is live. The top-level folders appear in the sidebar.

## Keeping your pack up to date

Footing evolves. New skills land and existing pages get sharpened. After your initial install, all updates happen through a skill that lives inside your vault, no marketplace refreshing, no plugin reinstalling, no Cowork restarting.

### How to trigger an update

1. Open Cowork and make sure it's pointed at your Footing vault folder. Cowork picks up the vault's skills automatically from the vault's `Skills/` folder.
2. In a Cowork chat, type:

   ```
   /footing-update
   ```

   Or ask in natural language: "update Footing", "pull the latest from the Footing repo", "see if there's anything new in Footing". Any of those triggers the same skill.

3. The skill goes straight to the public Footing repository on GitHub via a plain HTTPS request and compares what's there to what you have. It works out the state of every file: new on GitHub, changed upstream since you last pulled, edited locally, or in conflict (you've edited and so has upstream). You're told what's safe to apply automatically and asked what to do about anything you've personalised.
4. When it finishes, you'll see a short report of what was added, what was updated, what was merged, and what was left alone.

Your sector-landscape pages, built during setup, are yours. They're generated once at install time from live research, not pulled from the repo, so `/footing-update` never touches them.

### Why this works without any setup

The `/footing-update` skill lives at `Skills/footing-update/SKILL.md` inside your vault. It was placed there by the initial `/footing-setup` run. Cowork sees it the moment your vault is open. The skill makes a plain HTTPS request to the public Footing GitHub URLs, no GitHub account, no auth, no Terminal, no Git on your machine.

### How conflicts are handled

The update skill is a three-way reconcile. It tracks the SHA (the GitHub blob identifier) of every file at the moment it was last pulled to your vault, stored in `.footing/config.yml` under `last_known_shas:`. On each run, it compares three things per file: what was last pulled, what's currently on GitHub, and the SHA of the version sitting in your vault right now.

That tells it which of these situations each file is in:

- **Untouched both sides.** Skip, nothing to do.
- **Upstream-only change.** You haven't edited the file; upstream has. Safe to apply, applied by default with a chance to veto.
- **Local edit only.** You've edited; upstream hasn't changed. Skip, there's nothing new to bring in.
- **New on GitHub.** Add it.
- **Conflict.** You've edited the file AND upstream has new changes. You're asked per file: take theirs (overwrite local), keep mine (skip), or merge (the skill proposes a combined version that integrates upstream's changes into your edited file and asks you to confirm before writing).

Your personalised content is never overwritten without an explicit yes from you.

## Where your data lives

Your system will hold customer relationships, pricing and commercial detail, so this deserves a straight answer. Everything is files on your own computer, and nothing in the pack sends them anywhere: every skill is plain text you can read, none of them transmits data externally, and there is no MilUX server involved. When you work with the system through Cowork, the content you use in a session is processed by Claude under the terms of your Anthropic plan; read those terms and your plan's data settings before deciding what to keep in it, the same diligence you would apply to any supplier who processes your data.

Some things should not go in regardless: client material under a confidentiality agreement the client would not expect you to process with a cloud AI tool, sensitive personal data without a proper basis, and records your regulator requires kept in a controlled system. The installed pack carries a fuller page on all of this, including how the setup sits alongside Cyber Essentials and what to say when a client's security questionnaire asks.

## Yours, forever

Worth stating plainly, because everyone has been burned by a tool that died: your system does not depend on us. It is a folder of plain text files on your own computer, MIT licensed. Updates arrive over a plain HTTPS request to this public repository; there is no MilUX server or account in the loop. If Footing stopped being maintained tomorrow, everything you have would keep working exactly as it does today, and any text editor could still read it.

## What's next

In the first hour, focus on:

1. **Open `Context/<your name>.md`.** Check the operator profile reads well. Revise anything that needs sharpening.
2. **Read your sector-landscape pages**, if the setup skill built any, under `Intelligence/sector-landscape/`. They're a starting point for your own research, not a finished picture.
3. **Read the per-folder Guides.** Every folder has a `<Folder Name> Guide.md` at its root. Knowledge Guide, Operations Guide, Context Guide, and CRM Guide are the load-bearing ones.
4. **Connect Cowork to your vault.** Point Cowork at your new vault folder. Cowork and Obsidian now work against the same files; agents you run in Cowork write into the vault, and you see them in Obsidian.

## Running Footing in a small firm

Footing is built for a single operator first, and that is still the right way in. But many of the businesses it suits are five or ten people, so here is the pattern that works at that size. It is how MilUX, the firm behind the pack, runs its own version.

**Month one: one person.** Usually the owner, or whoever holds the customer relationships, because the daily brief, meeting prep and the sector pages serve that seat first. One Claude subscription. Prove the system earns its keep before involving anyone else.

**Month two: a second seat and a named curator.** The curator decides what becomes permanent. The system's value rests on its content being trustworthy, and that holds only if changes go through someone. In a small firm the curator is often the office or ops manager rather than the owner, and the weekly half-hour of review belongs to them. Everyone else's drafts land in a staging folder; the curator promotes what deserves to stay.

**Who actually needs to pay.** Only people driving the system through Cowork need a Claude subscription. Colleagues who just need to read it need neither a subscription nor Obsidian: the free [Vault Viewer](tools/vault-viewer/) reads everything in a browser. A realistic pattern for a seven-person firm is two or three subscriptions and the viewer for everyone else.

**What to bring in, and what to leave where it is.** Do not migrate your shared drive. The system is the working layer: strategy, relationships, engagements, your sector. Documents stay in the systems that already hold them, `/import-relationships` brings your living contacts across, and everything else earns its place one page at a time.

The mechanics once two or more people share the system:

- **Sync.** Obsidian Sync is the paid, no-setup option. A private Git repository is free and gives you version history, at the cost of a little setup. Pick one before two people are editing, not after; the pack's Sync and Backup page compares them.
- **Write boundaries.** Everyone can read everything; drafts land in staging; only the curator writes to the canonical folders. Keep agents on a tighter rein than people.
- **Updates.** `/footing-update` reconciles one vault against this repository. Agree that only the curator runs it, and avoid two people editing the same file in the same window.

None of this is needed on day one. Set the system up as a single operator, get value from it, and come back to this section when the second person is ready.

## Tools

Standalone tools that ship with Footing but install nothing live in [`tools/`](tools/).

- **[Vault Viewer](tools/vault-viewer/)** (v1.0.0). A single HTML file that reads a Footing vault, or any folder of Markdown notes, like a website. No install, no cloud, no Obsidian. Wikilinks, search and backlinks all work, and it runs fully offline with no network requests. Use it to hand a vault to someone who does not have Obsidian, or to read your own on a machine that does not. Download `tools/vault-viewer/vault-viewer.html`, open it in Chrome, Edge or Brave, and point it at a folder. See the [tool README](tools/vault-viewer/README.md) for detail.

## Share back

Footing gets better the more it's actually used. If a page reads oddly, a skill misfires, a question in the setup walkthrough doesn't fit your kind of business, or you hit a rough edge anywhere in the install, tell Matt. A line on LinkedIn, an email, or a screenshot will do. Fixes and improvements go into the next update so everyone else running the pack gets the benefit.

Email: matt@milux.co.uk. LinkedIn: [Matt Odell](https://www.linkedin.com/in/mattodell/).

## Troubleshooting

**The install skill leaves `{{placeholder}}` text in some files** — That's a bug. Tell Matt which files and which placeholder, and we'll fix it.

**Obsidian doesn't see the vault** — Make sure you point "Open folder as vault" at the Footing root, not at a subfolder.

**Anything else** — Email Matt at matt@milux.co.uk or open an issue at https://github.com/MilUX-Ltd/footing/issues.

## Help

- Email: matt@milux.co.uk
- GitHub issues: https://github.com/MilUX-Ltd/footing/issues
- LinkedIn: [Matt Odell](https://www.linkedin.com/in/mattodell/)

## Provenance

Footing is built by [Matt Odell](https://www.linkedin.com/in/mattodell/), founder of [MilUX](https://milux.co.uk), a user-centred design consultancy, and is the general-business sibling of MilUX's defence-sector pack, Foothold. The structure, conventions, and skills come from MilUX's own working vault: the system the company runs its business on, exported and made installable. When something in Footing improves, it is usually because it broke or fell short in real use first. It also improves with contributions from people running it; if you find something worth fixing or adding, see [Share back](#share-back).
