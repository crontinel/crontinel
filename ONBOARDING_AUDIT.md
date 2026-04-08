# Crontinel First-User Onboarding Audit

Date: 2026-04-08

---

## Discovery-to-First-Value Map

### The current journey (7 steps)

1. **Landing page** (crontinel.com) -- user reads hero, sees dashboard preview, understands the value prop
2. **Waitlist signup** -- enters email, gets "you're on the list" confirmation
3. **Wait** -- no immediate access; user cannot do anything until invited
4. **Registration** (app.crontinel.com/register) -- name, email, password (standard Breeze form)
5. **Onboarding wizard** (3 steps) -- team name, create app (name + timezone), install instructions with API key
6. **Package install** -- `composer require crontinel/laravel && php artisan crontinel:install`, add env vars
7. **First ping** -- scheduler runs, SaasReporter sends data, Livewire dashboard polls every 30s and shows it

**Time to first value: 10-15 minutes after getting access (but unknown wait time on waitlist).**

---

## Step-by-Step Findings

### 1. Landing Page

**What works well:**
- Hero headline is emotionally compelling ("silently broken for 3 days")
- Dashboard preview is concrete and specific, not abstract marketing
- Problem section with three failure modes is excellent
- Pricing is clear and the free tier lowers the barrier
- OSS callout at bottom establishes trust

**Issues found:**
- **CTA is "Get early access" (waitlist)** -- there is no way to start using the product immediately. The "Start free" and "Start 14-day trial" buttons on pricing cards link to `/#waitlist`, not to a registration page. Every CTA is a dead end that collects an email and makes the user wait.
- **GitHub link points to `crontinel/crontinel`** but the actual repo/package is `crontinel/laravel`. If the GitHub repo slug doesn't match the composer package name, users who click "View on GitHub" and then try to figure out the install command from the repo may be confused. Verify the GitHub org has the repo at that URL.
- **"Self-host for free" link** also points to `github.com/crontinel/crontinel` -- same potential mismatch.
- **No "Docs" link in the hero or nav.** The docs site (docs.crontinel.com) is never linked from the landing page above the fold. Users who want to evaluate before signing up have no quick path to technical documentation.
- **Install command shown but not actionable.** The `composer require crontinel/laravel` is displayed as passive gray text under the hero, but there's no "copy" button and no link to the quick-start guide explaining what to do after install.

### 2. Docs Quick-Start

**What works well:**
- Six numbered steps, each with one command. Very clear.
- Explicitly calls `php artisan migrate` as a separate step (the README and install command don't mention this -- see below).
- SaaS connection is clearly marked optional.

**Issues found:**
- **Step 2 says "creates the `crontinel_runs` migration"** but Step 3 says "Run migrations." The InstallCommand actually calls `$this->call('migrate')` internally, so migrations are already run during install. The docs tell the user to run `php artisan migrate` again, which is harmless but confusing -- it implies the install command didn't handle it.
- **No verification step.** After step 4 ("visit /crontinel"), there's no "you should see X" confirmation. A screenshot or description of the empty-state dashboard would help users confirm they succeeded.
- **No mention of `php artisan schedule:run`.** The OSS package's cron monitoring depends on Laravel's scheduler events. If the user doesn't have `schedule:run` in their crontab, cron monitoring produces zero data. The SaaS onboarding (install.blade.php) mentions this, but the docs quick-start does not.
- **No mention of Horizon.** If a user doesn't use Horizon, they'll see "No Horizon data" on the dashboard and might think something is broken. Quick-start should note: "Not using Horizon? Set `horizon.enabled = false`."

### 3. OSS README

**What works well:**
- Excellent README structure: what it monitors, requirements, install, config, alerts, all in one page
- Config example is complete and well-commented
- "Not using Horizon?" section is thoughtful
- SaaS upsell is tasteful and non-pushy

**Issues found:**
- **README says "php artisan crontinel:install" then "That's it. Visit /crontinel."** But the InstallCommand runs migrations internally. This is fine, except the README doesn't mention that migrations are being run. If a user runs this against a production database without realizing, they might be surprised.
- **README doesn't mention `php artisan migrate` at all.** The install command handles it, but this should be documented explicitly (e.g., "This command publishes config and runs migrations automatically").
- **`crontinel/php` is listed as `@dev` stability in composer.json.** The `oss/composer.json` requires `"crontinel/php": "@dev"`. If the php package isn't published to Packagist with a stable tag, `composer require crontinel/laravel` will fail for end users with default `minimum-stability: stable`. This is a blocker for first install.
- **GitHub badges link to `crontinel/crontinel` repo.** CI badge URL is `github.com/crontinel/crontinel/actions/workflows/ci.yml`. The composer package name is `crontinel/laravel` but the repo seems to be `crontinel/crontinel`. This needs to be consistent.

### 4. App Onboarding

**What works well:**
- Clean 3-step wizard with progress indicator (numbered circles with connecting lines)
- Step 1 (team name) is minimal -- gets users moving fast
- Step 2 (add app) asks only name and timezone -- no overload
- Step 3 (install) shows the exact API key inline, ready to copy
- The "I've installed it, take me to the dashboard" button is honest -- it doesn't pretend to verify

**Issues found:**
- **No copy-to-clipboard on the API key or install commands.** The onboarding install page shows `CRONTINEL_API_KEY=abc123` but there's no copy button. This is a miss -- users will need to manually select and copy a long key.
- **No verification/health-check.** Step 3 says "I've installed it" but doesn't verify. A "Test connection" button that pings the API would give users immediate confidence. The Livewire dashboard does poll (wire:poll.30000ms), but the user has to wait up to a minute after clicking through.
- **Timezone select in onboarding is hardcoded to 10 options.** The `onboarding/app.blade.php` has a fixed list of 10 timezones. The `apps/create.blade.php` (non-onboarding) uses `timezone_identifiers_list()` which gives all 400+. Users in unlisted timezones (e.g., America/Denver, Europe/Berlin, Asia/Singapore) will choose a wrong timezone during onboarding.
- **Registration form is unstyled Breeze default.** The `register.blade.php` uses `<x-guest-layout>` with default Breeze styling (light theme, gray-600 text). The rest of the app is dark-themed slate. This creates a jarring visual break between the dark landing page and a sudden light registration form.
- **No social auth (Google/GitHub).** For a developer tool, GitHub OAuth would reduce friction significantly.
- **Dashboard empty state after onboarding shows install instructions again.** If a user completes onboarding but hasn't sent the first ping yet, the Livewire component shows "Waiting for first ping..." with install instructions repeated. This is OK but slightly redundant -- the user just saw these exact commands on the previous page.

---

## Where It Feels Confusing or Incomplete

1. **The waitlist wall.** Every CTA leads to a waitlist. A developer who reads the landing page, loves the product, and wants to try it right now has no path forward. They can install the OSS package locally (which does work standalone), but the landing page doesn't make this path obvious.

2. **OSS vs SaaS confusion.** The landing page shows a SaaS dashboard mockup, talks about pricing tiers, and then at the bottom says "also free forever as an OSS package." The relationship between the two isn't immediately clear. Can you use just the OSS package and get the full dashboard? (Yes, locally.) Do you need the SaaS for alerts? (No, OSS has Slack/email alerts.) What does the SaaS actually add? (Multi-app view, history, team access.) This needs a clear comparison.

3. **`php artisan migrate` ambiguity.** The install command runs migrations. The docs say to run them separately. The README doesn't mention them at all. Three different messages about the same step.

4. **No "it's working" moment.** After install, users visit /crontinel and see data only if (a) Horizon is running, (b) queues have jobs, or (c) the scheduler has run at least once. For a fresh Laravel app with no queue activity, the dashboard will be empty. There's no synthetic "test" to trigger first data.

---

## Fastest Happy Path for an Early Laravel User

**Ideal path (what should exist):**
1. Land on crontinel.com, click "Start free"
2. Register with GitHub OAuth (10 seconds)
3. Onboarding: name team, name app, get API key
4. Run `composer require crontinel/laravel && php artisan crontinel:install`
5. Add `CRONTINEL_API_KEY=xxx` to `.env`
6. Run `php artisan schedule:run` once
7. See data in SaaS dashboard within 60 seconds
8. Total time: under 5 minutes

**Current path:**
1. Land on crontinel.com, join waitlist
2. Wait (days? weeks?)
3. Get invite email, register with email/password
4. Complete 3-step onboarding
5. Install package, add env vars, hope scheduler is running
6. Wait up to 60 seconds for first poll
7. Total time: unknown wait + 10-15 minutes

---

## Top 5 Friction Fixes (Ranked by Impact)

### 1. Remove the waitlist gate -- let users register immediately
**Impact: Critical. This is the single biggest blocker.**
Every CTA on the landing page sends users to a waitlist. No one gets value today. Change "Get early access" to "Start free" and link pricing buttons to `/register`. The free tier already exists at $0/forever. Let people use it.

### 2. Fix the `crontinel/php` `@dev` dependency
**Impact: Critical. First install will fail.**
The `oss/composer.json` requires `"crontinel/php": "@dev"`. Unless the user sets `minimum-stability: dev` in their own `composer.json`, `composer require crontinel/laravel` will fail with a stability error. Tag a stable release of `crontinel/php` (even `0.1.0`) and update the constraint.

### 3. Add a "Test connection" button on the onboarding install page
**Impact: High. Eliminates the "did it work?" anxiety.**
After the user adds the API key and runs install, provide a button that calls the `/api/ping` endpoint once and confirms "Connected! We received data from your app." This turns a 60-second uncertain wait into instant confirmation.

### 4. Fix the timezone mismatch in onboarding
**Impact: Medium. Affects users in ~390 of 400 timezones.**
Replace the hardcoded 10-timezone select in `onboarding/app.blade.php` with `timezone_identifiers_list()` (matching `apps/create.blade.php`). Add a search/filter since the full list is long. Wrong timezone means cron "late" detection will fire false positives.

### 5. Add docs link and copy buttons to the landing page and onboarding
**Impact: Medium. Reduces small frictions across the funnel.**
- Add "Docs" link to the landing page nav
- Add copy-to-clipboard on install commands and API keys in both the landing page and the onboarding install step
- Add `php artisan schedule:run` to the docs quick-start
- Standardize the migration messaging (InstallCommand runs them; docs should say "migrations run automatically")
