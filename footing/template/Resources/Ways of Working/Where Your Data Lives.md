---
type: guide
status: active
created: 2026-07-02
last_reviewed: 2026-07-02
tags: [data-handling, security, ways-of-working]
---

# Where Your Data Lives

This system will end up holding your customer relationships, your pricing, your plans and your view of your market. Before it does, you should be able to answer, for yourself and for anyone who asks, where that data actually goes. This page is the straight answer. Where it and Anthropic's own documentation disagree, their documentation wins; check it rather than trusting a summary that may have aged.

## The short version

The vault is a folder of plain files on your own computer. It has no server side. Nothing in the pack transmits your data anywhere: the skills are plain-text instructions you can open and read, they write only to the vault, and the update mechanism is a one-way fetch from a public GitHub repository. The one party that processes your content is Anthropic, when you work with the system through Claude, and that relationship is governed by your own plan's terms, not by anything Footing controls.

## What Claude sees

When you (or a scheduled task) work in Cowork, the content used in that session is sent to Anthropic for processing, like any cloud AI tool. What Anthropic may do with it depends on your plan and your settings. Do the diligence you would do on any supplier: read the [privacy policy](https://www.anthropic.com/legal/privacy) and your plan's commercial terms, and check your account's settings on whether conversations may be used for model improvement. If your firm has a data protection lead or an IT policy, this is the paragraph to show them.

Two practical consequences. First, Claude sees what a session touches, not the whole vault by default; a conversation about one customer does not upload your CRM. Second, the scheduled tasks this pack offers (daily brief, sector scan, curation sweep) run on your machine through your own Cowork and write only to the vault; none of them posts, emails or sends anything anywhere.

## What never goes in the vault

Whatever your plan's terms say, some material does not belong in this system at all:

- **Client material under a confidentiality agreement** beyond what the client would knowingly expect you to process with a cloud AI tool. When in doubt, ask them; the conversation is easier before than after.
- **Sensitive personal data** (health, and the other special categories under UK GDPR) without a recorded basis and a hard think about whether it needs to be here at all. The CRM convention tracks lawful bases per contact, `Resources/Business/Data Protection Basics.md` covers the ground, and the `build-dpia` skill exists for anything heavier.
- **Records your regulator requires kept in a controlled system.** If you work in a regulated sector, your sector pages probably name the regime; the vault is a working layer, not a system of record for regulated material.

## Sitting alongside Cyber Essentials

The vault is business data on an end-user device, and the usual controls apply to it like anything else: full-disk encryption on, screen lock on, the machine inside your patching and malware scope, and backups per [[Resources/Ways of Working/Sync and Backup|Sync and Backup]]. Claude and Obsidian are installed software, so they belong in your software inventory. The `cyber-essentials-ready` skill walks the device controls if you have not done them.

## When a client's security questionnaire asks

The honest answers, which are also good answers: business data is held as files on company-controlled, encrypted devices; the AI processor is Anthropic under a paid commercial plan, terms available; no third-party or pack-operated servers hold the data; the automation is plain-text instruction files, auditable on request; and updates are pulled from a public repository with nothing flowing back. Firms fail these questionnaires by not knowing, more than by any particular answer.

## Related

- [[Resources/Ways of Working/Sync and Backup|Sync and Backup]]
- [[Resources/Business/Data Protection Basics|Data Protection Basics]]
- [[Knowledge/tagging-policy|Tagging policy]] for the lawful-basis convention
