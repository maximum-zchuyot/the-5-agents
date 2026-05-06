# Image Generation Skill — Pointer

Yuval delegates image generation to:

→ `.claude/skills/gpt-image-gen/SKILL.md`

---

## What the skill does

Wraps the OpenAI Images API (`POST /v1/images/generations`) with model `gpt-image-2`.
Handles auth via `OPENAI_API_KEY` from `.env`, saves the raw API response to
`/tmp/openai_img_response.json`, then decodes the base64 payload to a PNG file.

Two decode paths:
- **Primary:** `curl | jq | base64 --decode` (fast, requires `jq`)
- **Fallback:** inline Python 3 (`json` + `base64` stdlib — no extra dependencies)

## Parameters expected by the skill

| Variable | Description |
|---|---|
| `OPENAI_API_KEY` | Loaded from `.env` |
| `PROMPT` | Full generation prompt |
| `OUTPUT_PATH` | Destination for the PNG (e.g. `yuval/outputs/2026-05-06-hero.png`) |
