# Contributing to Crontinel

Thank you for your interest in contributing to Crontinel!

## Code of Conduct

By participating, you are expected to uphold our [Code of Conduct](https://github.com/crontinel/crontinel/blob/main/CODE_OF_CONDUCT.md). Please report unacceptable behavior to **me@harunray.com**.

## How to Contribute

### Bug Reports

Search [existing issues](https://github.com/crontinel/crontinel/issues) first. If your bug hasn't been reported, [open a new issue](https://github.com/crontinel/crontinel/issues/new/choose) using the bug report template.

### Feature Requests

Search [existing issues](https://github.com/crontinel/crontinel/issues) for similar ideas. Use the feature request template to propose new functionality.

### Pull Requests

1. Fork the relevant repo (not this one — this is the meta repo)
2. Create a feature branch: `git checkout -b feat/my-feature`
3. Make your changes
4. Add tests if applicable
5. Ensure CI passes
6. Submit a PR with a clear description

### Repositories

- [`crontinel/app`](https://github.com/crontinel/app) — Hosted SaaS application
- [`crontinel/landing`](https://github.com/crontinel/landing) — Marketing site
- [`crontinel/docs`](https://github.com/crontinel/docs) — Documentation
- [`crontinel/php`](https://github.com/crontinel/php) — PHP core library
- [`crontinel/laravel`](https://github.com/crontinel/laravel) — Laravel package
- [`crontinel/node`](https://github.com/crontinel/node) — Node.js SDK
- [`crontinel/python`](https://github.com/crontinel/python) — Python SDK
- [`crontinel/go`](https://github.com/crontinel/go) — Go SDK
- [`crontinel/rust`](https://github.com/crontinel/rust) — Rust SDK
- [`crontinel/cli`](https://github.com/crontinel/cli) — CLI tool
- [`crontinel/mcp-server`](https://github.com/crontinel/mcp-server) — MCP server

## Development Setup

See individual repository README files for setup instructions.

## Coding Standards

- PHP: PSR-12 + Laravel Pint
- Node.js: ESLint + TypeScript strict
- Python: Ruff
- Go: `go vet` + `gofmt`
- Rust: `cargo fmt` + `cargo clippy`
