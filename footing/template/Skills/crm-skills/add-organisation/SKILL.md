---
name: add-organisation
description: Add a new organisation to the CRM. Pulls public information about the company, drafts an organisation page, asks the user to confirm before writing. Use when the user says "add an organisation", "add <company>", "capture <organisation>", "log this company", or runs /add-organisation. Handles clients, suppliers, partners, competitors, investors, and trade bodies. Bakes in the rebrand pattern (former_name frontmatter for renamed orgs) and the parent-folder pattern (for organisations that restructure, merge, or spin out units).
audited: 2026-07-01
audit_verdict: pass
audited_with: skill-safety-audit v3
origin: built
maintainer: MilUX
license: MIT
---

# add-organisation

USE WHEN the user runs `/add-organisation` or asks to capture a new organisation into the CRM. Distinct from `add-contact` (people) and `add-event` (events).

## Pre-flight

Confirm you're in a Footing pack: check that `CLAUDE.md` exists at the vault root and that `CRM/organisations/` exists. If not, suggest running `/footing-setup` first.

If the user said something like "add an organisation" without naming the company, ask: "Which organisation would you like to add?" and wait for the name (or a website URL).

## Phase A — Gather identity

Collect:

- **Organisation name.** Required. Use the canonical legal name where possible (e.g. "Acme Group plc"), with a shorter common form in the body if that's what they go by ("Acme").
- **Website.** Required if known. If the user only gave a name, look up the official site or ask.
- **Relationship type.** Required. One of: client, supplier, partner, competitor, investor, trade body.
- **Parent organisation.** Optional. If the new org is a subsidiary, department, or operating unit, capture the parent.
- **Former name(s).** Optional. If the org has been renamed.
- **Public LinkedIn page.** Optional but useful.
- **Public contacts.** Optional. Roles and named individuals only if they're publicly listed (About page, LinkedIn).

Accept paste: a website URL, a Companies House link, a LinkedIn company page, or free text.

## Phase B — Research

If a website was provided or you can derive one, call WebFetch on the home page and the About / Leadership pages. Extract:

- One-line description of what the company does.
- Industry or sector (a factual research field, not the CRM classification, e.g. "manufacturing", "professional services", "logistics").
- Size signal (employee count where stated).
- Public leadership (founders, CEO, MD, named directors).
- Headquarters location.
- Recent public news where directly relevant (contract or framework appointments, named partnerships, funding rounds).

If a Companies House URL is provided, fetch for incorporation date and registered office. If a LinkedIn company page is provided, fetch for headcount and public posts.

**Critical:** public information only. If the user wants to add private engagement context (deal value, internal contacts, NDA-bound content), do it in a separate body section, never in frontmatter, and confirm twice before writing.

## Phase C — Classify subfolder

Determine the destination subfolder from the relationship type, matching the default Footing taxonomy:

- `CRM/organisations/clients/` for the organisations and people who buy from you.
- `CRM/organisations/suppliers/` for vendors, contractors, and service providers you buy from.
- `CRM/organisations/partners/` for organisations you work alongside without a straightforward buy/sell relationship: referral, delivery, or integration partners.
- `CRM/organisations/competitors/` for public-information pages on who else operates in your space.
- `CRM/organisations/investors/` for venture capital firms, angel investors, or any other funding relationship, current or prospective. Once this set grows past comfortable single-folder browsing, use the eight letter-based subfolders (`0-9`, `A-B`, `C-D`, `E-H`, `I-N`, `O-R`, `S-T`, `U-Z`) that ship empty by default.
- `CRM/organisations/trade bodies/` for industry associations and sector representative groups.

If the vault's taxonomy has been adapted (a product business using `customers/` instead of `clients/`, for example), use Glob on `CRM/organisations/` to see what actually exists and ask the user where the new org belongs if it's not obvious.

## Phase D — Handle parent-child

If the user mentioned a parent organisation:

1. Check whether the parent exists in `CRM/organisations/`.
2. If yes, the new org goes inside the parent's folder. Pattern: `CRM/organisations/<relationship type>/<Parent Name>/<New Org Name>.md`. Set `parent:` in the new org's frontmatter to the parent's wikilink.
3. If no, ask the user: should the parent be created first, or should this org go at the relationship-type top level and the parent linkage be added later? Suggest creating the parent first if the user expects more children under it.

This pattern handles organisation restructures cleanly: when a larger client, supplier, or partner reorganises, merges, or spins out a unit, you can add child orgs into the parent folder without renaming or splitting existing pages.

## Phase E — Handle rebrand

If the user mentioned that the org has been renamed (or you found this in the research pass):

1. Capture the new name as the canonical page name and the H1.
2. Add `former_name: "<Old Name>"` to frontmatter.
3. Add a rename callout under the H1: `> Renamed <date> from <Old Name>. Source: <citation>.`
4. Do not create a separate page for the old name. One canonical page, one current identity.

If the rebrand also means the org now sits inside a different parent (a restructure that grouped child units under a new parent, for example), use the parent-folder pattern from Phase D too.

## Phase F — Draft

Draft the organisation page in memory. Use this shape:

```yaml
---
type: organisation
name: <Canonical Name>
status: active | dormant | alumni | target
website: <URL>
category: client | supplier | partner | competitor | investor | trade-body
created: <today, ISO>
parent: <wikilink to parent if applicable>
former_name: <old name if renamed>
tags: [<contextual tags>]
---

# <Canonical Name>

> Renamed <date> from <Old Name>. <Citation>. <If rebrand applies.>

## Company details

- **Website:** [<url-no-protocol>](<URL>)
- **Industry:** <the researched industry or sector, e.g. "manufacturing", "professional services">
- **Size:** <employee band if known>
- **Headquarters:** <city / country if known>
- **Founded:** <year if known>
- **Public leadership:** <names with roles, only if publicly listed>

## What <Name> does

<One or two paragraphs of public-info description. Drawn from the company's own about page or other public sources. Plain English.>

## Recent activity

<Recent publicly-known news if directly relevant: contract or framework appointments, named partnerships, funding announcements. Each item dated and sourced.>

## Key contacts

| Name | Role | Email |
|------|------|-------|
| [[CRM/contacts/active contacts/<Name>\|<Name>]] | <Role> | <Email if public> |

<Only include this table if there are publicly listed named individuals OR existing CRM contacts at this org. Use escaped pipes in wikilinks per R-01.>

## Source material

- <URLs cited above>

## Related

- <Sibling orgs, parent organisation, if relevant>
- <Frameworks they're on, networks they belong to, other organisations they're associated with>
```

Fill every field you have data for. Omit any section with no content.

## Phase G — Confirm

Show the draft to the user. Ask:

> "Here's the organisation page I'd write to `CRM/organisations/<path>/<Name>.md`. Anything to change before I save it?"

Wait for explicit confirmation or amendments.

## Phase H — Write

Write the file to the determined path. Use the canonical organisation name as the filename. For acronymic abbreviations, the convention is `Full Name (ACRONYM).md`.

## Phase I — Cross-reference

Check for related entities:

- **Contacts mentioned.** If named individuals appeared in the user's input or in the research pass, check whether they exist in `CRM/contacts/`. Suggest running `/add-contact` for any that don't.
- **Frameworks, portals, sector landscape.** If the user mentioned any (or the research pass surfaced public framework or programme appointments), check whether the relevant `Intelligence/sector-landscape/...` pages exist and link to them.
- **Parent / child orgs.** If you placed the new org inside a parent folder, ensure the parent page links back to the child.

Do not auto-create related entities. Suggest the user run the relevant skill, or do it themselves.

## Guidelines

- Public information only. Private engagement context goes in a clearly-marked body section and only with double confirmation.
- One canonical page per current organisational identity. Rebrands use `former_name:`, not parallel pages.
- Use the parent-folder pattern for organisation restructures and other parent-child relationships.
- Confirm before writing. Never write an organisation page without explicit user confirmation.
- Cross-reference into CRM/contacts/ and Intelligence/sector-landscape/ so the graph stays connected.
