---
type: guide
folder: Intelligence
---

# Intelligence Guide

## Purpose

`Intelligence/` is for external-facing scanning. The market you operate in, the wider landscape you sit inside, competitors, public literature. Anything you need to know about the outside.

The discipline is "this is for external scanning, not internal artefacts". Your own delivery artefacts, your own decisions, your own initiative pages do not live here. They live in `Initiatives/`, `Capabilities and Services/`, or `Context/`.

## Structure

```
Intelligence/
├── Intelligence Guide.md           (this file)
├── sector-landscape/
│   ├── Sector Landscape Index.md
│   ├── Programmes/
│   │   └── <Programme or scheme name>.md
│   ├── Frameworks/
│   │   └── <Procurement or commercial framework>.md
│   └── Portals/
│       └── <Portal name>.md
├── events/
│   └── <events you attend, see Events Guide>
├── market/
│   └── <Market topic>.md
├── competitors/
│   └── <Competitor name>.md
├── literature/
│   └── <Paper, report, article>.md
└── decisions/
    └── <External decision relevant to your market>.md
```

**`sector-landscape/`** holds public reference pages for your sector: the funding programmes, procurement routes, and portals relevant to what you do. Ships empty; populated live at setup by the sector-capture step, and grown from there as you learn your sector's specifics. The `Sector Landscape Index.md` at the root, once you create it, is a map page, not an entity home. Entities live in CRM (`CRM/organisations/`); the landscape pages map their relationships.

**`market/`** is broader market analysis: industry trends, sector reports, dynamics affecting your space.

**`competitors/`** is competitive analysis. One page per competitor, with public-info only. Engagement notes against competitors stay in their CRM page (if they're an organisation you also engage with directly).

**`literature/`** holds notes on public-domain papers, reports, articles you've read. Source material that informed your thinking.

**`decisions/`** holds external decisions (regulatory shifts, market announcements, policy changes) that affect your market. Different from internal decisions, which live with the initiative they belong to.

## Frontmatter

Frontmatter depends on the entity type. Common pattern for a sector-landscape entity:

```yaml
---
type: programme | framework | portal
status: active | retired
created: YYYY-MM-DD
website: https://...
parent: "[[Intelligence/sector-landscape/<parent>|<parent>]]"  # for child orgs
former_name: "<old name>"  # for rebrands
last_reviewed: YYYY-MM-DD
---
```

For market and literature pages:

```yaml
---
type: market | literature
created: YYYY-MM-DD
source: <URL or citation>
tags: [...]
---
```

## Add discipline

**Public information only.** Intelligence pages should be sourceable from public material: gov.uk or equivalent, company websites, LinkedIn public profiles, published reports. Anything you learned through a private relationship belongs in CRM, not here.

**Maps versus entities.** Index pages and landscape diagrams are maps, not entity homes. If a page has more than one entity's information, it's a map. If it has one entity's information, it's that entity's home. Maps live in `Intelligence/sector-landscape/`; entity homes live in the relevant CRM folder.

**Sector-landscape rebrands.** When a landscape entity restructures, use the parent-folder pattern: a folder named after the parent organisation, with renamed children inside carrying both the new title and `former_name:` frontmatter. Keep search continuity.

**Don't mirror CRM.** If you have a working relationship with a sector-landscape entity, that organisation lives in `CRM/organisations/`. The Intelligence page references the CRM page; it doesn't duplicate it.

## Canonical example

The shipped Footing defaults ship `sector-landscape/` empty; there is no pre-populated worked example, unlike Foothold's defence corpus. The setup skill's sector-capture step writes your first entries. For entity pages generally, follow the public-info shape: short company-style page with public mission, leadership where named publicly, website, and (where relevant) parent/child relationships via frontmatter.
