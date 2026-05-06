# Meeting Notes — Index

Code, architecture, decisions, and session logs. One file per topic, with Overview, Open Questions, and a chronological Session Log.

## Topics

- [[project-scaffold]] — initial commit: `CLAUDE.md`, `.gitignore`, `.env`/`.env.example`, the `.claude/` skeleton, first push to `origin/main`.
- [[superpowers-installation]] — manual install of the `obra/superpowers` skills library (v5.1.0, 14 skills) into `.claude/skills/`.
- [[obsidian-vault-bootstrap]] — exposing the obsidian skills at the canonical path, wiring SessionStart + UserPromptSubmit hooks, scaffolding `vault/`.
- [[ceo-agent-scaffold]] — CEO Agent system prompt + four sub-agent stubs, CLAUDE.md routing update.
- [[yuval-agent-gpt-image-gen]] — Yuval creative image agent + gpt-image-gen skill (OpenAI Images API wrapper); CEO promoted to flat file `reuven.md`.
- [[yael-content-writer-agent]] — Yael content writer sub-agent; rewrites raw articles in brand style; IMAGE_NEEDED placeholder protocol for Yuval integration.
- [[chen-web-researcher-agent]] — Chen web research sub-agent; searches the internet, filters quality sources, saves findings to Content/ as input for Yael.
