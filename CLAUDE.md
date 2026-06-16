# MOB-Composite Monorepo

This is a monorepo of 4 git submodules. Each subdirectory is an independent git repository with its own history.

## Subprojects

| Directory | Tech | Purpose |
|-----------|------|---------|
| `WhatNot-Webhook-Holder/` | Go 1.22 | REST API backend |
| `Whatnot-Frontend/` | Next.js 14 (TypeScript) | Admin web UI |
| `WhatNot-Username-Parser/` | JavaScript (Tampermonkey) | Browser userscript for Whatnot platform |
| `No-Mod-Livestream/` | Markdown only | Design docs and feature specs — no code |

## Data Flow

```
Whatnot.com → Userscript → POST /webhook/product_sold → Backend API ↔ PostgreSQL
                                                                    ↕
                                                              Frontend UI
```

## How Services Connect

- Frontend calls backend via the `BACKEND_HOST` environment variable
- Auth: credentials stored in browser `localStorage`, sent as `Authorization: Basic <base64>` on every API request
- Backend port is set via `port` env var (default local: `5555`)

## Domain Vocabulary

- **Channel** — a Whatnot seller account / streaming channel
- **Stream** — a single livestream session
- **Break** — a collection of mystery boxes within a stream
- **Event** — one buyer's team slot purchase within a break

## Notes

- No tests in any subproject
- No CI/CD pipeline
- No shared Makefile or root docker-compose — each subproject has its own
