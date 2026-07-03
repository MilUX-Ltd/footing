# Footing — Structure and How It Works

This document explains what's inside a Footing pack, how it's organised, and how setup and updates work. Read it once at install time so you know what you're working with.

## What you get

A Footing pack is a working Obsidian vault. Open it in Obsidian and the structure is already in place: folders for your operator profile, your contacts and organisations, your initiatives, your reference library, and an intelligence layer that gets a short set of sector-specific reference pages written into it at setup time. You don't start from a blank vault, and you don't start from someone else's sector either. You start from a structure that already knows how a business runs, populated with research specific to yours.

The pack ships in three layers.

**Structure.** Folder layout, page templates, frontmatter conventions, and skills. The load-bearing part. It changes slowly and you inherit it as an opinionated default.

**Live-researched sector content.** Unlike a pack that ships the same pre-populated reference material to everyone, Footing's sector-landscape pages are generated for you, once, during setup, from a live round of research into your specific sector. Nobody else's vault has the same pages.

**Stubs and rules.** Empty page templates plus a documented rule, per folder, for how you grow your own knowledge base.

## The folder structure

```
Your Pack/
├── CLAUDE.md
├── Home.md
├── Capabilities and Services/
├── Context/
├── CRM/
├── Customer Engagements/
├── Daily/
├── Ideas/
├── Initiatives/
├── Intelligence/
├── Knowledge/
├── Marketing/
├── Operations/
├── Resources/
└── Skills/
```

The pack is a flat top-level. No nested namespaces. Wikilink paths stay short and the mental model stays simple.

### Per-folder intent

**Capabilities and Services.** What your organisation sells and what it runs internally. Splits into `Customer-Facing Services/` for paid offers and `Internal Services/` for operational functions like Content Pillars, Content Creation Workflow, and Compliance Service. Ships with a Guide explaining the split and a canonical example service stub.

**Context.** Your own profile, brand, strategy, team, stakeholders. The root files are templated stubs populated with your details at install time. Each ships with a worked example so you see what a well-formed page looks like.

**CRM.** Contacts, organisations, and networks. `CRM/organisations/` splits by relationship type: `clients/`, `suppliers/`, `partners/`, `competitors/`, `investors/`, `trade bodies/`. That's a deliberate difference from a sector-specific CRM pattern built around one particular kind of external body; an established business's contact book spans all of these relationship types from day one, not just one.

**Daily.** Standard Obsidian daily-notes pattern. Ships with a daily-note template and a Guide explaining how to use it. Wire up daily briefings or signal scans as you add agent integrations of your own.

**Ideas.** A capture-quickly, process-later inbox. Ships with a Guide that defines what belongs (early-stage ideas, sparks) and what doesn't (anything with a natural home elsewhere), so it doesn't drift into a junk drawer.

**Customer Engagements.** Work you deliver for someone else. Each engagement maps 1:1 to an organisation page in `CRM/organisations/clients/`. Three-state lifecycle (`scoping/`, `active/`, `completed/`) reflecting how customer work actually moves: shaped, agreed, delivered. Ships with `Customer Engagements Guide.md` carrying the canonical Guide pattern and the binary rule that distinguishes engagements from initiatives.

**Initiatives.** Work you do for yourself. Internal services, your own products, marketing, thought leadership, operating-model change, internal tooling. Two-state lifecycle (`active/`, `completed/`). Ships with `Initiatives Guide.md` carrying the canonical Guide pattern, the cross-link to Customer Engagements, and the binary split rule: outcome owned by your business → Initiative, outcome owned by an external organisation → Customer Engagement.

**Intelligence.** External-facing scanning: events, and `sector-landscape/` (`Frameworks/`, `Portals/`, `Programmes/`). Unlike a pre-populated version of this folder, Footing's `sector-landscape/` ships empty and is filled once, at setup, by the `footing-setup` skill's live research pass, scoped to the sector you name. The Guide codifies the "this is for external scanning, not internal artefacts" rule so the folder stays clean.

**Knowledge.** Agent operating rules: the rules file, frontmatter conventions, tagging policy. Distinct from Resources, which is your practitioner reference library. Knowledge files are policy documents your agents read at runtime.

**Marketing.** Marketing Outputs (published artefacts and active drafts) and Newsletter content. Footing's three-layer marketing pattern keeps strategy in `Capabilities and Services/Internal Services/Content Pillars.md`, workflow in `Capabilities and Services/Internal Services/Content Creation Workflow.md`, and outputs here in Marketing. Marketing is a function you run.

**Operations.** Load-bearing for the agent stack. Ships pre-populated with your email-signature stub and runtime policy files your agents read at message-send time. The Guide spells out the in-scope test ("would removing it break a live agent flow?") and lists what doesn't belong here.

**Resources.** Your practitioner reference library. Ships with a six-subfolder structure: `Methods/`, `Ways of Working/`, `Books/`, `Business/`, `Frameworks/`, `Reference/`, `Templates/`. Each subfolder has its own Guide explaining what belongs.

**Skills.** The agent skills that ship with the pack, organised into `pm-skills/` (business-method reference skills), `business-skills/`, `crm-skills/`, `content-skills/`, `brand-skills/`, and `meta-skills/`. Skills are executable. The content they draw on lives elsewhere in the vault.

## The Guide pattern

Every major folder ships with a `<Folder Name> Guide.md` at its root. The Guide is the contract for what belongs in the folder.

Every Guide carries five sections:

1. **Purpose.** One paragraph. What this folder is for.
2. **Structure.** What each subfolder means.
3. **Frontmatter.** Required and optional fields per page type.
4. **Add discipline.** How to add new content. Points at the relevant skill if one exists.
5. **Canonical example.** A worked reference page so you can see what good looks like.

When you're not sure where something goes, read the relevant Guide. When you can't decide between two folders, the Guide tells you.

## Templating

Footing uses placeholders for everything specific to you. The `footing-setup` skill fills them in during install, from your answers to the setup questions.

| Placeholder | Meaning |
|-------------|---------|
| `{{pack_name}}` | The display name of your pack |
| `{{pack_slug}}` | Slugified pack name for paths |
| `{{pack_owner}}` | Your full name |
| `{{pack_owner_first}}` | Your first name |
| `{{pack_owner_email}}` | Your primary email |
| `{{pack_org}}` | Your organisation |
| `{{pack_org_slug}}` | Slugified organisation name |

A small `.footing/config.yml` in the pack root tracks the current substitution values, your sector, and the SHA of every file as last pulled from GitHub, used by `/footing-update`'s three-way reconcile.

## How setup and updates work

There is no bash installer and no separate plugin. Both setup and update are Cowork skills that fetch plain files over HTTPS from the public GitHub repo. See the README for the full walkthrough; in outline:

**`footing-setup`** (run once, via the one-line prompt in the README). Lays down the folder structure, asks seven onboarding questions, runs the sector research pass into `Intelligence/sector-landscape/` if you named a sector, offers a context drop, builds your canonical pages from the answers and any material you supplied, and offers to schedule `/footing-update` on a cadence.

**`/footing-update`** (run any time, manually or on a schedule). Compares your vault against the current state of the GitHub repo using the SHA history in `.footing/config.yml`, and reconciles file by file: applies upstream-only changes automatically, leaves your own edits alone, adds anything new, and asks you to resolve genuine conflicts. It never touches `Intelligence/sector-landscape/`; that content was generated for you specifically and isn't part of the shared repo.

## One operator, agents with boundaries

Footing is built for a single operator working with Cowork, and that is how it should be run first. What ships alongside that is a set of conventions that keep agent work disciplined as you add more of it: operating rules in `Knowledge/` that agents read at runtime, policy and signature assets in `Operations/`, agent-owned sections in daily notes, and a drafts-then-promotion pattern for anything that becomes canonical. When a second person or a second agent arrives, the same conventions carry the write boundaries; the README's small-firm section describes that path. The conventions work directly with Cowork and can be adapted to other AI tools without changing the structure; how you wire your agents in is your choice. Footing is opinionated about the boundaries, and the implementation underneath is yours.

## The skill set

Around sixty skills ship with the pack, in seven categories. The high points:

- **meta-skills.** The pack's own lifecycle and hygiene: `footing-setup`, `footing-update`, `sector-scan` (re-runs your install-time sector research monthly and reports what changed), `daily-brief` (writes your morning brief), `curator` (a budgeted monthly hygiene sweep), `skill-safety-audit` (run on any skill from outside before it runs, no exceptions), `skill-value-review`, `prompt-master`, `process-interviewer`.
- **crm-skills.** The high-frequency adds and their payoff: `add-contact`, `add-organisation` (classified by relationship type, with rename support), `add-event` (with a Chatham House Rule check at intake), `meeting-prep`, `mobilise-engagement`, and `import-relationships` for bringing your existing CRM across, connector-first, with triage so only living relationships come in.
- **business-skills.** `write-sow`, `cyber-essentials-ready`, `build-dpia`, `red-team-investor`, `late-payment-reminder`.
- **pm-skills.** Twenty-six business-method reference skills (prioritisation, positioning, research synthesis, competitive analysis, pricing, personas, pre-mortems and more), stripped of sector-specific framing so they apply to whatever business you run.
- **ops-skills.** The operations wing for an established business: `process-map`, `sop-capture`, `service-blueprint`, `ai-readiness`.
- **brand-skills.** `design-system-setup`, which builds your design system from your onboarding answers.
- **content-skills.** `newsletter-writer` and `humaniser`.

Every skill carries audit frontmatter (`audited`, `audit_verdict`, `origin`, `maintainer`), and the audit discipline applies to anything you add from elsewhere.

## What ships in the sector-landscape layer

Nothing, at repo level. That is the point of difference from a pack that ships one pre-populated reference layer for everyone. Footing's `Intelligence/sector-landscape/` is empty in the public repo and gets filled, per install, by `footing-setup`'s live research pass, scoped to the sector you name during onboarding: an overview page always, plus a framework or portal page where one genuinely applies. Skip the sector question and the folder stays empty; nothing is guessed or filled with placeholder content.

The content rule for that research is the same discipline as everything else in the pack: public, searchable sources only (the sector body's own website, gov.uk, trade press), cited, and built fast, a handful of searches per page rather than an exhaustive review.

## Growing your pack

The discipline is simple. Per-folder Guides are the contract. Skills cover the high-frequency adds (contacts, organisations, events). The long tail follows the conventions documented in each Guide.

When in doubt:

- Read the Guide for the folder you're working in.
- Copy the shape of the canonical example referenced in the Guide.
- If you can't place something, ask your agent.

The pack works because the conventions are kept tight. Adding things off-pattern is the fastest way to break it.
