---
type: guide
folder: CRM/organisations
---

# Organisations Guide

## Purpose

`organisations/` holds organisations you have or might have a working relationship with. Split by relationship type so the structure scales as the set grows and stays useful regardless of sector.

## Structure

- **`clients/`.** The organisations and people who buy from you.
- **`suppliers/`.** Vendors, contractors, and service providers you buy from.
- **`partners/`.** Organisations you work alongside without a straightforward buy/sell relationship: referral partners, delivery partners, integration partners.
- **`competitors/`.** Public-information pages on who else operates in your space.
- **`investors/`.** Venture capital firms, angel investors, or any other funding relationships, current or prospective. Split into eight letter-based subfolders (`0-9`, `A-B`, `C-D`, `E-H`, `I-N`, `O-R`, `S-T`, `U-Z`) once the set grows past comfortable single-folder browsing.
- **`trade bodies/`.** Industry associations and sector representative groups relevant to you.

Adapt these subfolders to how your business actually works. A product business might prefer `customers/` to `clients/`; a business with a complex supply chain might split `suppliers/` further. Change the taxonomy deliberately and record the deviation in `Knowledge/rules.md`.

## Writing an organisation

- Add via the `/add-organisation` skill where available; it pulls public info, drafts the page, asks you to confirm before writing. To write one by hand, insert the [[Templates/Organisation|Organisation template]].
- For organisations with parent-child structures (a holding company with subsidiaries, a department with subsidiary units), use the parent-folder pattern: a folder named after the parent organisation, with each child page inside carrying `parent:` in frontmatter pointing at the parent page.
- When an organisation rebrands, write the renamed page with `former_name:` in frontmatter and a one-line rename note under the title. Do not keep parallel pages for old and new identities. This matters most for organisations that reorganise or rebrand on a multi-year cadence.
- Engagement history (meetings, decisions, what they're working on) belongs on active organisation pages. The page is more than a directory entry.

## Lifecycle

An organisation's `status:` is one of `active`, `target`, `alumni` or `dormant`. A `target` becomes `active` when you start working with them. An `active` organisation becomes `alumni` when the relationship has finished and `dormant` when it has gone quiet. The status does not decide the folder; the relationship type does.

## Frontmatter

Follows the parent CRM Guide:

```yaml
---
type: organisation
name: <canonical name>
status: active | target | alumni | dormant
created: YYYY-MM-DD
updated: YYYY-MM-DD
website: https://...
category: client | supplier | partner | competitor | investor | trade-body
parent: "[[CRM/organisations/.../<parent>|<parent>]]"   # for child orgs
former_name: "<old name>"                                # for rebrands
tags: []
---
```

`category:` should match the subfolder (`client`, `supplier`, `partner`, `competitor`, `investor`, `trade-body`). `parent:` and `former_name:` used as needed.

## Canonical example

Start from the [[Templates/Organisation|Organisation template]]. A finished page carries the frontmatter above, a short description, a key contacts table (with escaped pipes in wikilinks, per `Knowledge/rules.md`), engagement history and public links.

## Related

- [[CRM/CRM Guide|CRM Guide]] — parent
- [[CRM/contacts/Contacts Guide|Contacts Guide]] — sibling
- [[CRM/networks/Networks Guide|Networks Guide]] — sibling
- [[Templates/Templates Guide|Templates Guide]]: the note templates
