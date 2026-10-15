# Footing: words and what they mean

The glossary for this repository.

| Word | Meaning here |
|---|---|
| Footing | The pack: this repository, and the knowledge system it installs. From "get your footing", standing on solid ground. |
| Pack | The installable whole: template, skills, plugin and setup. Footing and Foothold are sibling packs. |
| Foothold | The sibling pack for defence-sector founders (`MilUX-Ltd/foothold`). Changes to shared skills usually land in both. |
| Template | `footing/template/`: the files a user's vault receives at setup and update. |
| Vault | The user's installed copy of the template, a folder of Markdown opened in Obsidian. The README calls it the user's "system" or "knowledge base". |
| Setup | `footing-setup`: lays the vault down from the template in the Footing plugin and runs onboarding. Offline. |
| Update | `/footing-update`, the vault-bundled skill that compares the vault with `main` on GitHub and pulls changed template files without overwriting the user's own work. |
| Sector-landscape pages | Reference pages about the user's own sector, researched live at setup and written into their vault. Not shipped in the template. |
| `last_known_shas` | The update skill's record of each template file's git blob SHA at the last install or update, used to tell a user's edit from an upstream change. |
| `{{pack_owner}}` | The placeholder replaced with the user's name at setup. Files carrying it are listed by hand in the update skill. |
| Guide file | The `<Folder> Guide.md` page in every template folder, saying what goes there. |
| Skill | A `SKILL.md` folder under `Skills/` that Claude runs inside the vault. |
| Cowork | Anthropic's desktop app in which the pack is designed to run alongside Obsidian. |
| Release | A version heading in `CHANGELOG.md`. What users receive is whatever is on `main`. |
