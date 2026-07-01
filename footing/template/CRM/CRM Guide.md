---
type: guide
folder: CRM
---

# CRM Guide

## Purpose

`CRM/` is the people and organisations you have or might have a working relationship with. Distinct from `Intelligence/sector-landscape/`, which is the public map of who-is-who in your sector. Sector-landscape pages point at CRM entries; CRM is where each entity actually lives.

The discipline of CRM is what makes the rest of the vault valuable. Contact pages carry the relationship knowledge that lets {{pack_owner_first}} (and {{pack_owner_first}}'s agents) move fast: who knows who, what conversations have happened, what's outstanding, what's been agreed. Without that, your vault is a filing cabinet. With it, it's a working second-brain.

## Structure

```
CRM/
├── CRM Guide.md                (this file)
├── contacts/
│   ├── active contacts/
│   ├── reference contacts/
│   └── archive/
├── organisations/
│   ├── clients/
│   ├── suppliers/
│   ├── partners/
│   ├── competitors/
│   ├── investors/
│   └── trade bodies/
└── networks/
    ├── <Formal Network>/
    ├── <Peer Network>/
    └── <Identity Network>/
```

### contacts/

People you interact with. Three subfolders:

- **`active contacts/`** — people you have current or recent contact with. The page captures what you know about them: role, organisation, how you met, what they care about, conversations to date, things outstanding.
- **`reference contacts/`** — people you may not know personally but who matter to your domain: industry figures, named subject-matter experts, public officials whose moves affect your space. No relationship intelligence; these are pointer pages.
- **`archive/`** — people you no longer interact with. Pages preserved for search but flagged inactive.

### organisations/

Organisations split by relationship type, not by sector. The default subfolders work for most established businesses:

- **`clients/`** — the organisations and people who buy from you.
- **`suppliers/`** — vendors, contractors, and service providers you buy from.
- **`partners/`** — organisations you work alongside without a straightforward buy/sell relationship: referral partners, delivery partners, integration partners.
- **`competitors/`** — public-information pages on who else operates in your space.
- **`investors/`** — if relevant. Split into eight letter-based subfolders (`0-9`, `A-B`, `C-D`, `E-H`, `I-N`, `O-R`, `S-T`, `U-Z`) once the set grows past comfortable single-folder browsing.
- **`trade bodies/`** — industry associations and sector representative groups relevant to you.

Adapt these subfolders to how your business actually works. A product business might want `customers/` rather than `clients/`; a business with a long supply chain might want to split `suppliers/` further. Change the taxonomy deliberately and record the deviation in `Knowledge/rules.md`.

### networks/

Networks of people you belong to or engage with. Three flavours, each documented in a separate subfolder:

- **Formal networks** — defined memberships with a coordinator and a clear list (industry working groups, sector clusters, formal advisory boards).
- **SME peer networks** — informal but recurring groupings of founders and operators (peer learning groups, founder dinners, mastermind cohorts).
- **Identity networks** — groupings based on shared identity rather than formal structure (Reservists, Veterans, alumni networks, professional certifications). These are powerful for trust-based introductions but light on formal coordination.

Each network has its own subfolder with an index page listing the network's purpose, members or member-clubs where public, the coordinator if there is one, and any standing engagements.

## Frontmatter

### contacts

```yaml
---
type: contact
status: active | reference | inactive | archived
created: YYYY-MM-DD
organisation: "[[CRM/organisations/<category>/<org>|<org>]]"
role: "<their current role>"
linkedin: https://...
email: ...
phone: ...
lawful_basis: legitimate-interests | consent | contract | legal-obligation
tags: [...]   # include the matching lb-* tag, e.g. lb-legitimate-interests
---
```

`lawful_basis:` records the UK GDPR Article 6 basis on which you process the contact's personal data. Every contact has exactly one; mirror it with an `lb-*` tag. See `Knowledge/tagging-policy.md` for the four bases and when each applies.

### organisations

```yaml
---
type: organisation
status: active | target | alumni | dormant
created: YYYY-MM-DD
website: https://...
category: client | supplier | partner | competitor | investor | trade-body
parent: "[[CRM/organisations/.../<parent>|<parent>]]"   # for child orgs
former_name: "<old name>"                                # for rebrands
tags: [...]
---
```

### networks

```yaml
---
type: network
flavour: formal | peer | identity
status: active | dormant
created: YYYY-MM-DD
coordinator: "[[CRM/contacts/active contacts/<name>|<name>]]"
platform: "<where the network meets>"
---
```

## Add discipline

### Contacts

The `add-contact` skill is the primary way to add a contact. It pulls public information, drafts the page, and asks you to confirm before writing. Long-tail additions follow the same shape manually.

**Active vs reference.** If you have a working relationship or a recent conversation, the contact is active. If you just need a pointer page for someone you don't directly engage with, it's reference. Don't fudge the line: active pages carry relationship intelligence that reference pages should not.

**Archiving.** Move a page from `active contacts/` to `archive/` when the relationship has ended. Don't delete: search continuity matters and old context is often useful later.

### Organisations

The `add-organisation` skill handles standard adds. Two patterns earn special attention:

**Rebrands and restructures.** When an organisation is renamed or restructured, the right pattern is one page per current identity, not parallel pages for old and new. Each renamed page carries:

- A `former_name:` frontmatter entry preserving the old name for search.
- A rename callout under the title citing the source announcement.
- The original page content preserved under a "Historical content (pre-rename)" section if it carries useful context, otherwise migrated into the body and the old page deleted.

This matters most for organisations that reorganise or rebrand on a multi-year cadence, larger clients and suppliers with corporate structures that shift over time.

**Parent-child structures.** When a parent organisation has named children (a holding company with operating subsidiaries, a department with subsidiary units), use a parent-named folder containing both the parent page and each child:

```
clients/
└── Acme Holdings/
    ├── Acme Holdings.md          (parent)
    ├── Acme Manufacturing.md     (child)
    ├── Acme Logistics.md         (child)
    └── ...
```

Children carry `parent:` in frontmatter pointing at the parent page. This absorbs reorganisations cleanly: when the parent restructures, you adjust the parent page and the child pages without breaking inbound wikilinks to children.

**Engagement history.** Active organisation pages capture engagement history: meetings, decisions, what they're working on, what's outstanding. This is the relationship knowledge that makes CRM worth maintaining. Lose it and the folder becomes a directory.

### Networks

Add networks deliberately. A network page exists when there's a coordinator, a list of members, a platform where the network communicates, and a reason to track engagement across all of those at once. A loose Slack channel of acquaintances is not yet a network; promote it to one when patterns become persistent.

## Canonical example

See `CRM/organisations/<category>/<canonical example>.md` for the canonical organisation page shape: frontmatter, executive summary, products or services, key contacts table (using escaped pipes in wikilinks per `Knowledge/rules.md`), recent engagement, outstanding items, public links.

For contacts, see `CRM/contacts/active contacts/<canonical example>.md`: one-paragraph biography, role and organisation, how you met, conversation history, outstanding items, public links.
