---
type: guide
folder: CRM/organisations
---

# Organisations Guide

## Purpose

`organisations/` holds organisations you have or might have a working relationship with. Split by relationship type so the structure scales as the set grows and stays useful regardless of sector.

## Subfolders

- **`clients/`.** The organisations and people who buy from you.
- **`suppliers/`.** Vendors, contractors, and service providers you buy from.
- **`partners/`.** Organisations you work alongside without a straightforward buy/sell relationship: referral partners, delivery partners, integration partners.
- **`competitors/`.** Public-information pages on who else operates in your space.
- **`investors/`.** Venture capital firms, angel investors, or any other funding relationships, current or prospective. Split into eight letter-based subfolders (`0-9`, `A-B`, `C-D`, `E-H`, `I-N`, `O-R`, `S-T`, `U-Z`) once the set grows past comfortable single-folder browsing.
- **`trade bodies/`.** Industry associations and sector representative groups relevant to you.

Adapt these subfolders to how your business actually works. A product business might prefer `customers/` to `clients/`; a business with a complex supply chain might split `suppliers/` further. Change the taxonomy deliberately and record the deviation in `Knowledge/rules.md`.

## Add discipline

- Add via the `/add-organisation` skill where available; it pulls public info, drafts the page, asks you to confirm before writing.
- For organisations with parent-child structures (a holding company with subsidiaries, a department with subsidiary units), use the parent-folder pattern: a folder named after the parent organisation, with each child page inside carrying `parent:` in frontmatter pointing at the parent page.
- When an organisation rebrands, write the renamed page with `former_name:` in frontmatter and a one-line rename note under the title. Do not keep parallel pages for old and new identities. This matters most for organisations that reorganise or rebrand on a multi-year cadence.
- Engagement history (meetings, decisions, what they're working on) belongs on active organisation pages. The page is more than a directory entry.

## Frontmatter

Follows the parent CRM Guide. `category:` should match the subfolder (`client`, `supplier`, `partner`, `competitor`, `investor`, `trade-body`). `parent:` and `former_name:` used as needed.

## Related

- [[CRM/CRM Guide|CRM Guide]] — parent
- [[CRM/contacts/Contacts Guide|Contacts Guide]] — sibling
- [[CRM/networks/Networks Guide|Networks Guide]] — sibling
