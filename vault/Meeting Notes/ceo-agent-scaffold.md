# CEO Agent Scaffold

## Overview

Creates the top-level orchestrator agent for the `the-5-agents` content creation team. The CEO Agent is defined at `.claude/agents/ceo-agent/agent.md` and is the mandatory entry point for all user tasks — it decides whether to handle a request directly or delegate to one of four specialist sub-agents. Four placeholder sub-agents (`agent-1` through `agent-4`) are scaffolded with TBD roles; their full PRDs are forthcoming. `CLAUDE.md` is minimally updated to surface the routing flow at the top.

## Open Questions

- The four sub-agent roles are undefined. Each will require its own PRD before it can be delegated to. Until then, the CEO handles all tasks directly.
- The CEO's `## Available Sub-Agents` table will need updating as follow-up PRDs arrive — add the role and "Invoke When" column for each agent once defined.

## Session Log

### 2026-05-06 — CEO Agent and sub-agent stubs created [shipped]
- **What was done:**
  - Followed the PRD (CEO Agent / Main Orchestrator) to design and implement the agent scaffold.
  - Created `.claude/agents/ceo-agent/agent.md` with full system prompt:
    - 5-step decision protocol: Understand → Assess → Block → Execute/Delegate → Final Output
    - Quality review checklist for sub-agent outputs (5 criteria)
    - Available sub-agents table (all TBD until follow-up PRDs)
    - Communication style rules (answer-first, one question at a time, no padding)
  - Created stub `agent.md` files for agents 1–4 in `.claude/agents/agent-{1,2,3,4}/`.
  - Updated `CLAUDE.md` with a new "כיצד עובדת המערכת" section at the top, showing the routing flow: `משתמש → CEO Agent → לבד / Agent-1-4`. Existing content left intact.
  - Created this vault topic file and added it to the Meeting Notes index.
- **Decisions:**
  - **`.claude/agents/` not root `agents/`.** CLAUDE.md and Claude Code conventions both place agents at `.claude/agents/`; a root `agents/` dir would require extra wiring and diverge from the existing project guide.
  - **English for agent.md.** Consistent with the superpowers skills library (all English); CLAUDE.md stays Hebrew.
  - **CEO alone until sub-agents are defined.** The PRD explicitly marked sub-agents as TBD; the CEO system prompt instructs to handle all tasks directly until the table is filled.
  - **Minimal CLAUDE.md update.** PRD said "don't recreate claude.md from this PRD" — interpreted as: preserve existing content, prepend one new section only.
- **Notes / Caveats:**
  - Files and owners:
    - `.claude/agents/ceo-agent/agent.md` — project (authored per PRD)
    - `.claude/agents/agent-{1,2,3,4}/agent.md` — project (stubs)
    - `CLAUDE.md` — user (updated minimally)
  - Claude Code discovers custom agents in `.claude/agents/<name>/agent.md` automatically; no additional wiring needed for the CEO to appear as an available agent type.
- **Related:** [[project-scaffold]], [[obsidian-vault-bootstrap]]
