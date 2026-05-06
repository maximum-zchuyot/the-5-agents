# Superpowers Installation

## Overview

Manual installation of the `obra/superpowers` v5.1.0 skills library into `.claude/skills/`. Upstream ships only `skills/` at the top level — no `commands/` or `agents/` — so 14 skills were copied and nothing else. The skills cover brainstorming, planning, TDD, debugging, code review, parallel agent dispatch, and worktree workflows. Status: shipped to `origin/main` (commit `1ee00c2`).

## Open Questions

- Upstream is pinned at v5.1.0 by virtue of `git clone --depth 1` of `main` on 2026-05-06; no automatic update mechanism. If a new Superpowers release matters, manually re-clone and copy.

## Session Log

### 2026-05-06 — Manual install via git clone + cp [shipped]
- **What was done:**
  - Cloned `https://github.com/obra/superpowers.git` shallow into a temp dir; inspected layout.
  - Verified no name collisions in `.claude/skills/` before copying.
  - `cp -rn skills/* .claude/skills/` (no-clobber to be safe; nothing pre-existed under those names).
  - 14 skill folders added under `.claude/skills/`:
    - [[brainstorming]], [[dispatching-parallel-agents]], [[executing-plans]], [[finishing-a-development-branch]] (notes for these as standalone topics may follow if used heavily)
    - [[receiving-code-review]], [[requesting-code-review]], [[subagent-driven-development]], [[systematic-debugging]]
    - [[test-driven-development]], [[using-git-worktrees]], [[using-superpowers]], [[verification-before-completion]]
    - [[writing-plans]], [[writing-skills]]
  - Each skill folder has a `SKILL.md` plus, in some cases, sub-files (prompts, scripts, examples). Sub-file inventory lives inside each skill folder; not duplicated in the vault.
  - Commit `1ee00c2`, pushed to `origin/main`.
  - Cleaned up temp clone.
- **Decisions:**
  - Did NOT use Claude Code's `/plugin` system — the user's harness does not have plugins enabled.
  - Did NOT run `claude`, `npm`, or `gh` — none guaranteed in the user's PATH; only `git` and `bash` were used.
  - Did NOT touch existing `.claude/` files — copy was strictly additive (`cp -rn`).
  - Did NOT copy `commands/` or `agents/` — upstream does not ship them.
- **Notes / Caveats:**
  - Files: every file under `.claude/skills/<superpowers-skill-name>/` belongs to the **Superpowers** project (Jesse Vincent / `obra`), MIT-licensed. The user is the **owner** of the choice to install; upstream remains the **author**.
  - Push to `main` succeeded without re-prompt — Windows Credential Manager held the token from the prior commit's auth.
  - Git issued LF→CRLF warnings on Windows; benign.
- **Related:** [[project-scaffold]]
