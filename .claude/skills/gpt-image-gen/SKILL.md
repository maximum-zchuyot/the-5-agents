---
name: gpt-image-gen
description: >
  Generate a PNG image from a text prompt using the OpenAI Images API (gpt-image-2).
  Reads OPENAI_API_KEY from .env. Uses curl + jq primary path with a Python
  fallback for environments where jq is unavailable.
---

# gpt-image-gen

Generate an image via the OpenAI Images API and save it as a `.png` file.

## Prerequisites

- `OPENAI_API_KEY` set in `.env`
- `curl` available (standard on macOS / Linux / Git Bash on Windows)
- `jq` **or** Python 3 for base64 decoding

---

## Step 1 — Load the API key

```bash
export OPENAI_API_KEY=$(grep -E '^OPENAI_API_KEY=' .env | cut -d= -f2-)
```

If the key is empty, stop and tell the user to add `OPENAI_API_KEY=<key>` to `.env`.

---

## Step 2 — Call the API, save raw response

```bash
curl -s -X POST "https://api.openai.com/v1/images/generations" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "gpt-image-2",
    "prompt": "'"$PROMPT"'",
    "size": "1024x1024",
    "quality": "medium",
    "output_format": "png"
  }' > /tmp/openai_img_response.json
```

> Replace `$PROMPT` with the actual prompt string before running. If the prompt
> contains special characters, write the JSON body to a temp file and pass it
> with `-d @/tmp/openai_img_body.json` instead.

---

## Step 3 — Decode base64 → PNG

### Option A: jq (preferred, faster)

```bash
jq -r '.data[0].b64_json' /tmp/openai_img_response.json \
  | base64 --decode > "$OUTPUT_PATH"
```

### Option B: Python fallback (use when jq is not available)

```bash
python3 - <<'PYEOF'
import json, base64, os, sys

with open('/tmp/openai_img_response.json') as f:
    data = json.load(f)

# Check for API error
if 'error' in data:
    print(f"API error: {data['error']}", file=sys.stderr)
    sys.exit(1)

b64 = data['data'][0]['b64_json']
output_path = os.environ['OUTPUT_PATH']

with open(output_path, 'wb') as f:
    f.write(base64.b64decode(b64))

print(f"Saved {os.path.getsize(output_path)} bytes → {output_path}")
PYEOF
```

> `OUTPUT_PATH` must be exported before running the Python block:
> `export OUTPUT_PATH="yuval/outputs/2026-05-06-hero.png"`

---

## Step 4 — Verify

```bash
if [ -s "$OUTPUT_PATH" ]; then
  echo "OK — $(wc -c < "$OUTPUT_PATH") bytes written to $OUTPUT_PATH"
else
  echo "ERROR — file missing or empty at $OUTPUT_PATH"
  echo "--- API response ---"
  cat /tmp/openai_img_response.json
  exit 1
fi
```

---

## Common API errors

| HTTP / field | Cause | Fix |
|---|---|---|
| `401` | Invalid or missing API key | Check `OPENAI_API_KEY` in `.env` |
| `400 content_policy` | Prompt violated policy | Rephrase the prompt |
| `429` | Rate limit exceeded | Wait and retry |
| `data[0].b64_json` missing | Unexpected response format | Check raw `/tmp/openai_img_response.json` |
