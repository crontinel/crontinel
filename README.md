# Crontinel

**Open-source monitoring for cron jobs, background workers, and scheduled tasks.**

Crontinel catches what generic uptime tools miss — the job that started but crashed silently, the queue worker that stopped processing, the cron that fired but did nothing.

---

## Ecosystem

Crontinel is available across your entire stack:

| Package | Description | Status |
|---------|-------------|--------|
| [`crontinel/php`](https://github.com/crontinel/php) | PHP core library | ![CI](https://img.shields.io/badge/CI-passing-brightgreen) |
| [`crontinel/laravel`](https://github.com/crontinel/laravel) | Laravel integration | ![CI](https://img.shields.io/badge/CI-passing-brightgreen) |
| [`crontinel/node`](https://github.com/crontinel/node) | Node.js SDK | ![CI](https://img.shields.io/badge/CI-passing-brightgreen) |
| [`crontinel/python`](https://github.com/crontinel/python) | Python SDK | ![CI](https://img.shields.io/badge/CI-passing-brightgreen) |
| [`crontinel/go`](https://github.com/crontinel/go) | Go SDK | ![CI](https://img.shields.io/badge/CI-passing-brightgreen) |
| [`crontinel/rust`](https://github.com/crontinel/rust) | Rust SDK | ![CI](https://img.shields.io/badge/CI-passing-brightgreen) |
| [`crontinel/ruby`](https://github.com/crontinel/ruby) | Ruby SDK | ![CI](https://img.shields.io/badge/CI-passing-brightgreen) |
| [`crontinel/cli`](https://github.com/crontinel/cli) | CLI tool | ![CI](https://img.shields.io/badge/CI-passing-brightgreen) |
| [`crontinel/mcp-server`](https://github.com/crontinel/mcp-server) | MCP server | ![CI](https://img.shields.io/badge/CI-passing-brightgreen) |
| [`crontinel/status-page`](https://github.com/crontinel/status-page) | Status page | — |

## Hosting

| Service | URL | Description |
|---------|-----|-------------|
| App | [app.crontinel.com](https://app.crontinel.com) | Hosted SaaS |
| Status | [status.crontinel.com](https://status.crontinel.com) | Public status page |
| Docs | [docs.crontinel.com](https://docs.crontinel.com) | Full documentation |
| Landing | [crontinel.com](https://crontinel.com) | Marketing site |

## Quick Start

Install the PHP package:

```bash
composer require crontinel/php
```

Or the Laravel package:

```bash
composer require crontinel/laravel
```

See [docs.crontinel.com](https://docs.crontinel.com) for full setup instructions.

## Features

- **Process-level monitoring** — not just "is the server up?" but "are your workers actually working?"
- **Laravel Horizon support** — reads worker state directly from Redis
- **Background job tracking** — knows when jobs start, finish, and fail
- **Smart alerting** — alerts go where your team works (Slack, email, webhooks, PagerDuty)
- **Self-hostable** — MIT licensed, run it on your own infrastructure

## License

MIT © Harun R Rayhan
