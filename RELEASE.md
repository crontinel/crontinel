# Crontinel Release Checklist

## Current State

| Package | Repo | Packagist/npm name | Latest tag |
|---|---|---|---|
| `crontinel/php` | `crontinel/php` | `crontinel/php` | _(none — never released)_ |
| `crontinel/laravel` | `crontinel/crontinel` (local: `oss/`) | `crontinel/laravel` | `v0.2.0` |
| `@crontinel/mcp-server` | `crontinel/mcp-server` | `@crontinel/mcp-server` | _(none — never published)_ |

---

## One-Time Setup (do before first release of each package)

### Packagist — `crontinel/php`
- [ ] Go to packagist.org → Submit → enter `https://github.com/crontinel/php`
- [ ] On the package page: API Tokens → copy the token
- [ ] In GitHub `crontinel/php` → Settings → Webhooks → Add webhook:
  - URL: `https://packagist.org/api/github?username=<packagist-user>`
  - Secret: the Packagist API token
  - Events: "Just the push event"

### Packagist — `crontinel/laravel`
- [ ] Verify the package is already registered at `https://packagist.org/packages/crontinel/laravel`
- [ ] Confirm the GitHub webhook in `crontinel/crontinel` is pointing to the correct Packagist user/token after the org move (Settings → Webhooks)
- [ ] Confirm `support.source` and `support.issues` in `oss/composer.json` point to `github.com/crontinel/crontinel` (already done)

### npm — `@crontinel/mcp-server`
- [ ] Ensure the `@crontinel` npm org exists and your account is a member: `npm org ls crontinel`
- [ ] Log in: `npm login`
- [ ] First publish (see release flow below)

---

## Release Flows

### 1. `crontinel/php`

> No `version` field in `composer.json` — Packagist derives version from git tags. Keep it that way.

```bash
cd /Users/ray/Work/crontinel/php

# 1. Make sure main is clean and tests pass
git status
composer test

# 2. Tag
git tag v0.1.0   # use next semver
git push origin v0.1.0

# 3. Packagist auto-updates via webhook within ~30 seconds.
#    If it doesn't, manually trigger:
#    packagist.org → crontinel/php → Update (button)
```

---

### 2. `crontinel/laravel`

> **Before tagging**, fix the dev dependency on `crontinel/php`.

```bash
cd /Users/ray/Work/crontinel/oss

# 1. Update crontinel/php constraint in composer.json
#    Change: "crontinel/php": "@dev"
#    To:     "crontinel/php": "^0.1.0"   (or whatever version was just released)
#
#    Also remove the repositories[] path-repo block:
#    Delete the entire:
#      "repositories": [{ "type": "path", "url": "../php", ... }]

# 2. Lint + test
composer install
composer test
vendor/bin/pint
git add composer.json composer.lock
git commit -m "release: update crontinel/php constraint to ^X.Y.Z"

# 3. Tag and push
git tag v0.3.0   # next semver after v0.2.0
git push origin main
git push origin v0.3.0

# 4. Packagist auto-updates via webhook (crontinel/crontinel repo).
```

**Checklist before tagging:**
- [ ] `"crontinel/php": "@dev"` replaced with a real version constraint
- [ ] `repositories` path-repo block removed from `composer.json`
- [ ] `composer.lock` committed (or deleted if you want lock-file-free)
- [ ] Tests green

---

### 3. `@crontinel/mcp-server`

```bash
cd /Users/ray/Work/crontinel/mcp-server

# 1. Bump version (edits package.json and creates a git tag automatically)
npm version patch   # or minor / major

# 2. Build + publish (prepublishOnly runs `npm run build`)
npm publish --access public

# 3. Push commit + tag that npm version created
git push origin main
git push origin --tags
```

> `npm version` creates a `vX.Y.Z` commit and tag. Don't manually tag in this repo.

---

## Repo / Org Checks After GitHub Org Move

- [ ] `crontinel/php` — webhook to Packagist installed (see one-time setup above)
- [ ] `crontinel/crontinel` — existing Packagist webhook still valid (token not rotated, URL correct)
- [ ] `crontinel/mcp-server` — no webhook needed for npm; publish is manual
- [ ] All three repos are public in the `crontinel` GitHub org
- [ ] `support.source` URLs in both `composer.json` files resolve correctly

---

## Post-Release Verification

### `crontinel/php`
```bash
# Check Packagist shows the new tag (allow ~1 min)
curl -s https://packagist.org/packages/crontinel/php.json | jq '.package.versions | keys'

# Install in a throwaway project
mkdir /tmp/test-php && cd /tmp/test-php
composer init --no-interaction
composer require crontinel/php
```

### `crontinel/laravel`
```bash
curl -s https://packagist.org/packages/crontinel/laravel.json | jq '.package.versions | keys'

mkdir /tmp/test-laravel && cd /tmp/test-laravel
composer create-project laravel/laravel . --quiet
composer require crontinel/laravel
php artisan vendor:publish --tag=crontinel
```

### `@crontinel/mcp-server`
```bash
# Check registry
npm view @crontinel/mcp-server version

# Smoke-test the binary
npx @crontinel/mcp-server --help
# or
npx -y @crontinel/mcp-server
```

---

## Versioning Convention

| Scenario | Bump |
|---|---|
| Bug fix, doc update | `patch` |
| New feature, backwards-compatible | `minor` |
| Breaking API change | `major` |

Keep `crontinel/php` and `crontinel/laravel` version numbers in sync (not required, but reduces confusion). `@crontinel/mcp-server` versions independently.
