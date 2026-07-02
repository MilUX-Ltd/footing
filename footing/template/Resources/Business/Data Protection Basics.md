---
type: reference
status: active
created: 2026-07-01
source: "ICO, 'A guide to lawful basis' and 'Getting started with data protection', https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/lawful-basis/, checked 2026-07-01"
tags: [fundamentals, data-protection, gdpr]
---

# Data Protection Basics

This is deliberately thin: enough to know what you're dealing with and whether you need to go further. Not legal advice. For anything genuinely high-risk, or if you're unsure, take proper advice or use the `build-dpia` skill shipped with this pack.

## What counts as personal data

Any information relating to an identified or identifiable living person. Names and email addresses are the obvious cases, but it also covers things like an IP address, a job title combined with an employer, or notes about a conversation with someone, if it lets you (or anyone else) work out who the person is. Most CRM contact pages in this vault contain personal data by this definition.

## Lawful basis, in brief

UK GDPR requires a lawful basis for every use of personal data. As of the ICO's April 2026 guidance update, there are seven recognised bases in total, but most day-to-day business use, holding contacts, running a client relationship, invoicing, falls under one of four. This pack's CRM already tracks these four on every contact (see `Knowledge/tagging-policy.md`):

- **Legitimate interests.** The default for ordinary B2B relationship-holding: prospects, network contacts, partners. Most contacts sit here. Requires a genuine business reason, weighed against the person's own interests, not a blank cheque.
- **Consent.** The person actively opted in to a specific use, such as a newsletter sign-up. Must be freely given, specific, and easy to withdraw.
- **Contract.** Processing necessary to deliver a contract with the person, or steps before one: clients, associates, contractors.
- **Legal obligation.** Processing required by law: accounting records, tax records, statutory reporting.

The other three (vital interests, public task, and the newer "recognised legitimate interest" category for a narrow set of pre-approved purposes) rarely apply to a small business's routine operations. If one of them seems relevant, that's a signal to look closer rather than to guess.

## When you need a DPIA and when you don't

A Data Protection Impact Assessment is a documented assessment of how you process personal data, the risk it creates for people, and what you do to reduce it. It's a legal requirement under UK GDPR Article 35 for processing likely to result in high risk to people, and good practice more widely.

You probably don't need one for ordinary CRM record-keeping, invoicing, or standard supplier and client management. You should do one if you're introducing something that involves large-scale processing, systematic monitoring, special category data (health, biometric, and similar), or anything that combines data in a way that could be intrusive if it went wrong.

If you're not sure which side of that line you're on, that uncertainty is itself the reason to run one. Use the `build-dpia` skill: it reads what your vault already knows, asks about the gaps, and produces a DPIA in the ICO's own structure.

## The one habit worth keeping

Record the lawful basis on every contact when you add them, not retrospectively. The `add-contact` skill does this by asking; it takes seconds at the point of creation and is genuinely hard to reconstruct later.

## Where to go for more

The ICO's own guidance is the primary source and is kept current: [A guide to lawful basis](https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/lawful-basis/a-guide-to-lawful-basis/) and [Getting started with data protection](https://ico.org.uk/for-organisations/advice-for-small-organisations/getting-started-with-gdpr/getting-started-with-data-protection/). Both are aimed at small organisations, not specialists.
