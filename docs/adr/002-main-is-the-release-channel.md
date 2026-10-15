# ADR 002: `main` is the release channel, so it is protected

Status: accepted, 15 October 2026 (card 7020). Records how the pack already works.

## Context

A new user's first prompt fetches `footing/skills/footing-setup/SKILL.md` from `main` and
follows it, and `/footing-update` reads the file tree of `main` from the GitHub API and pulls
every changed file under `footing/template/` into the user's vault. There is no release branch,
tag or staging copy between a merge and the next install or update.

## Decision

Treat `main` as the release channel. It is protected: changes arrive by pull request only, the
`checks` job must pass, force pushes and deletion are refused, and the rule applies to
administrators too. A change to `footing/template/` or to the setup skill is reviewed as a
release would be.

## Consequences

- A broken template file reaches users on their next update, and a broken setup skill reaches
  the next person to install, so the review of either is the release review.
- Other files (this documentation, `tools/`, `.github/`, `.claude/`) are never copied into a
  user's vault, so repository housekeeping does not reach users.
- If a staging step is ever wanted, the update skill would read a tag or a release branch
  instead of `main`; that is a new decision superseding this one.
