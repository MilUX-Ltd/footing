# Lessons

Mistakes already paid for on this pack, so nobody pays for them twice: what happened, why, and
the rule that came out of it. `LESSONS-INDEX.md` lists them one line each; regenerate it with
`python3 Workspace/agent-config/scripts/lessons-index.py <repository>` in the same commit.
`tools/check.py` fails when the two are out of step.

1. **A synced vault copy pushed by a timer is not a source** (card 7020)
   Until September 2026 the pack was edited in an Obsidian vault and a launchd job committed
   whatever it found and pushed it to `main` every four hours. Edits made on the Mac mini to
   `cyber-essentials-ready` never reached GitHub and had to be pushed by hand at the 29 September
   cut-over (commit 312dca2). After that the job's paths vanished and it stopped without a word,
   while the vault copy carried on under synoia in `Open/Packs` with nothing publishing it. Rule:
   GitHub is the only source (ADR 001). Work in a clone, change by pull request, and never
   reintroduce a sync job.

2. **The timer published a local index to a public repository** (card 7020)
   The job ran `git add -A`, so synoia's local index of the folder (`.context/index.sqlite`, a
   full-text copy of the notes, and `.context/config.json`, with the synoia organisation and
   channel identifiers) was committed and pushed with everything else. Rule: `.context/` is
   ignored and `tools/check.py` refuses it, with the other local files (Obsidian workspace state,
   `.trash/`, `.DS_Store`, database files). Add files by name, not with `git add -A` over a
   folder something else also writes to.

3. **Setup fetched the template as JSON it could not read** (Footing 2.1.0)
   `footing-setup` listed the template through the GitHub `git/trees` API, which returns JSON
   that the Cowork WebFetch tool cannot read. The file list came back empty and the install
   stalled before writing anything, while single raw-file fetches worked and hid the cause.
   The 2.1.0 fix made setup read a template bundled in an installed plugin, but the install is
   one prompt with no plugin, so the fix swapped one broken route for another (risk R5). Rule:
   setup and update fetch plain files by raw URL, never JSON through WebFetch; check any change
   to setup against the one-prompt design in `docs/architecture.md` before it ships.
