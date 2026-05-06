# Obsidian Vault Bootstrap

## Overview

Wires the project to use the `obsidian-vault-workflow` skill (and siblings `obsidian-markdown`, `obsidian-bases`) as Claude Code's long-term memory. The user dropped the three skills into `.claude/skills/` inside timestamped wrapper folders (`obsidian-*-20260506T115*-3-001/<inner>/SKILL.md`) which Claude Code's auto-discovery does not scan. Canonical copies were placed at `.claude/skills/<name>/SKILL.md` so the harness now lists them as available skills. A project-shared `.claude/settings.json` adds two hooks — `SessionStart` and `UserPromptSubmit` — that nudge Claude to invoke the workflow at session start and on every prompt. The `vault/` tree is initialized with the four canonical folders the skill mandates (`Meeting Notes/`, `Content Briefs/`, `Publishing Log/`, `Brand Guidelines/`) and their `_index.md` files. Status: shipped.

## Open Questions

- The original timestamped wrapper folders (`obsidian-*-20260506T115*-3-001/`) still exist alongside the canonical copies. They are inert (Claude Code only loads from the canonical paths) but clutter `.claude/skills/`. Decide whether to delete the wrappers in a follow-up — left untouched here per the standing "do not modify pre-existing `.claude/` files" rule.
- The `UserPromptSubmit` hook injects a reminder on **every** user prompt. Intentional per the user's request, but it adds context to even trivial prompts. Re-evaluate cadence if it becomes noisy.
- `vault/Content Briefs/`, `vault/Publishing Log/`, `vault/Brand Guidelines/` are empty stubs — populate as actual content / publishing / brand work begins.

## Session Log

### 2026-05-06 — Skill exposure, hooks, vault scaffold [shipped]
- **What was done:**
  - Read the user-supplied [[obsidian-vault-workflow]] `SKILL.md`. Mandates: topic-file-per-task, `## Overview` + `## Open Questions` + `## Session Log` structure, append dated `### YYYY-MM-DD — title [status]` entries at the bottom, `[[wikilinks]]` only for intra-vault refs, verify by Read-back.
  - Read sibling skills [[obsidian-markdown]] (Obsidian-flavored MD: wikilinks, callouts, embeds, properties, math, mermaid) and [[obsidian-bases]] (`.base` files for database-style views — not used yet).
  - Copied each skill's inner folder to its canonical discovery path:
    - `.claude/skills/obsidian-vault-workflow/SKILL.md` (owner: user / project)
    - `.claude/skills/obsidian-markdown/SKILL.md` (owner: user / project)
    - `.claude/skills/obsidian-bases/SKILL.md` (owner: user / project)
    - The original `obsidian-*-20260506T115*-3-001/` wrappers were left in place (additive copy, not move).
  - Created `.claude/settings.json` (owner: project, committed) with:
    - `SessionStart` hook (`startup|resume|clear`) emitting a reminder to run Phase 1 of the workflow.
    - `UserPromptSubmit` hook emitting a reminder to invoke the skill before responding.
  - Scaffolded `vault/` with the four canonical folders the skill defines, each with an `_index.md`:
    - `vault/Meeting Notes/_index.md` (this folder's index — lists [[project-scaffold]], [[superpowers-installation]], [[obsidian-vault-bootstrap]])
    - `vault/Content Briefs/_index.md` (empty stub)
    - `vault/Publishing Log/_index.md` (empty stub)
    - `vault/Brand Guidelines/_index.md` (empty stub)
  - Wrote retroactive topic files documenting prior work: [[project-scaffold]] and [[superpowers-installation]]. Each enumerates the files it touched, who owns them, and links to related topics.
  - Wrote this topic file ([[obsidian-vault-bootstrap]]) and added it to [[Meeting Notes/_index|the Meeting Notes index]].
- **Decisions:**
  - **Topic granularity.** The user asked for "one MD per file"; the skill mandates "one MD per topic". Resolved by writing per-topic files (per the skill) where each topic's Session Log enumerates every file it touches with path, role, and ownership. This satisfies the skill literally and the user's intent (every file is documented and cross-linked to related topics).
  - **Skill exposure via copy, not move.** The user previously instructed "do not modify pre-existing `.claude/` files." Copy preserves originals. Duplicates can be cleaned up in a follow-up if desired.
  - **Hooks placement.** Project-shared `.claude/settings.json` (committed), not `settings.local.json` — the workflow is a project-level rule that should apply to anyone working on this repo, not one machine.
  - **Hook payload.** Plain `echo` strings (cross-shell safe on bash/cmd/PowerShell). Hook stdout is appended as additional Claude context.
- **Notes / Caveats:**
  - When Claude Code first reads the new `settings.json`, the user will be prompted to approve the hooks once — expected.
  - The skill's protocol is enforced both by the hooks (per-prompt reminder) and by the skill's own description (auto-suggested by Claude Code's skill matcher when relevant).
  - Files documented this session and their owners:
    - `.claude/skills/obsidian-vault-workflow/SKILL.md` — user (sourced from upstream tarball-style folder)
    - `.claude/skills/obsidian-markdown/SKILL.md` — user
    - `.claude/skills/obsidian-bases/SKILL.md` — user
    - `.claude/settings.json` — project (added this session)
    - `vault/Meeting Notes/_index.md`, `vault/Content Briefs/_index.md`, `vault/Publishing Log/_index.md`, `vault/Brand Guidelines/_index.md` — project
    - `vault/Meeting Notes/project-scaffold.md`, `vault/Meeting Notes/superpowers-installation.md`, `vault/Meeting Notes/obsidian-vault-bootstrap.md` — project
  - `.obsidian/` files (`app.json`, `appearance.json`, `core-plugins.json`, `graph.json`, `workspace.json`) are user-controlled vault preferences — left untouched.
- **Related:** [[project-scaffold]], [[superpowers-installation]]
