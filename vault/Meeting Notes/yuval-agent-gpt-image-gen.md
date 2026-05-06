# Yuval Agent & gpt-image-gen Skill

## Overview

Yuval is the project's creative image-generation agent, built on top of the `gpt-image-gen` skill which wraps the OpenAI Images API (`gpt-image-2`). The agent follows a 7-step workflow: scan `yuval/reference/` for style cues, craft a prompt combining user intent + reference style, generate via the skill, save the PNG + sibling `.txt` prompt file to `yuval/outputs/`, verify, and report. The hybrid layout places the canonical Claude agent definition at `.claude/agents/yuval.md` (flat file) and the working directories (`reference/`, `outputs/`) at `yuval/` in the project root. The CEO agent was also promoted to a flat file at `.claude/agents/reuven.md` with Yuval registered as the first active sub-agent.

## Open Questions

- `gpt-image-2` model ID — confirm availability in the OpenAI API; may need to fall back to `gpt-image-1` if not yet released.
- `yuval/outputs/` and `yuval/reference/` are currently tracked by git — consider adding to `.gitignore` if binary assets grow large.
- `ceo-agent/agent.md` (subdirectory CEO stub) now coexists with `reuven.md` (flat file CEO) — consolidate when convenient.

## Session Log

### 2026-05-06 — Bootstrap Yuval agent + gpt-image-gen skill [shipped]
- **What was done:** Created `.claude/skills/gpt-image-gen/SKILL.md` (curl + jq primary path, Python fallback); created `.claude/agents/yuval.md` (flat file, 7-step workflow); scaffolded `yuval/reference/`, `yuval/outputs/`, pointer docs `yuval/agent.md` + `yuval/skill.md`; created `.claude/agents/reuven.md` as the canonical flat-file CEO agent with Yuval registered in "Sub-Agents Under Your Command"; added `OPENAI_API_KEY=` to `.env` and `.env.example`.
- **Decisions:** Flat-file agent layout chosen per user spec (Claude Code discovers flat `.md` files in `.claude/agents/`, not subdirs). CEO renamed `reuven.md` to match the project's naming convention; `ceo-agent/agent.md` left intact as legacy. Reference/outputs dirs use `.gitkeep` to commit the structure without content.
- **Notes / Caveats:** The exposed OpenAI API key in the user message should be rotated at platform.openai.com. Model `gpt-image-2` used as specified — verify availability.
- **Related:** [[ceo-agent-scaffold]], [[project-scaffold]], [[obsidian-vault-bootstrap]]
