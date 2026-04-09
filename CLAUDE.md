# Crontinel Workspace  -  CLAUDE.md

This is the root of the Crontinel workstream. All active repos live as subdirectories.

## Repos

| Directory | Repo | Description |
|---|---|---|
| `oss/` | `crontinel/oss` | MIT Laravel package  -  ships to Packagist |
| `landing/` | `crontinel/landing` | Astro landing page (crontinel.com) |
| `app/` | `crontinel/app` (private) | SaaS application |

## Working across repos

```bash
cd oss/      # OSS package work
cd landing/  # Landing page work
cd app/      # SaaS app work (when created)
```

Each subdirectory has its own `.git` and its own `CLAUDE.md`  -  read it before working there.

## Isolation rules

- Never commit files from subdirectories into this workspace repo  -  they are excluded via `.gitignore`
- This repo tracks workspace-level files only (this CLAUDE.md, shared docs, etc.)
- Never mix repo contexts without an explicit `/ws switch`

## Response Footer (Telegram / OpenClaw)

Every message sent to the user in Telegram must end with:

```
⏰ ct || 🤖 {model}
```

One blank line before the footer. No exceptions.
