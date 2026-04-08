# Crontinel — Before-Launch Checklist

Last updated: 2026-04-08
Based on: ONBOARDING_AUDIT.md, DNS_AUDIT.md, PRICING.md, RELEASE.md, WAITLIST.md, WAITLIST_FALLBACK.md, app/docs/server-setup.md

Legend: `P0` = launch blocker | `P1` = launch-week must | `P2` = nice-to-have before or just after launch

---

## 1. Product

### App Features
- [ ] `P0` Registration page is accessible without a waitlist gate — all "Start free" and "Start 14-day trial" pricing buttons link to `/register`, not `/#waitlist`
- [ ] `P0` Free tier works end-to-end: register → onboard → install OSS package → see first ping on dashboard
- [ ] `P0` 14-day Pro trial starts automatically on registration (no CC required); `TrialExpiredMail` fires at expiry and drops plan to Free
- [ ] `P0` `PlanLimits::canCreateApp()` returns a clear upgrade prompt UI when limit is hit (not a silent failure)
- [ ] `P1` GitHub OAuth registration added (developer tool — GitHub OAuth reduces signup friction significantly)
- [ ] `P1` Registration form (`register.blade.php`) styled to match the dark slate theme, not Breeze default light theme
- [ ] `P1` Dashboard empty-state copy does not repeat install instructions verbatim after onboarding completion; shows a distinct "Waiting for first ping..." state
- [ ] `P2` Stripe products and prices created: Pro Monthly ($19), Pro Yearly ($182), Team Monthly ($49), Team Yearly ($470)
- [ ] `P2` `STRIPE_WEBHOOK_SECRET` set in production `.env`; all ten Cashier webhook events registered in Stripe dashboard

### Trial / Billing
- [ ] `P0` `config/cashier.php` wired to real Stripe Price IDs (not placeholders)
- [ ] `P1` Trial-to-paid nudge email sequence defined and tested (at minimum: day 12 warning, day 14 expiry)
- [ ] `P1` Upgrade/downgrade between Pro and Team works without data loss
- [ ] `P2` Annual pricing toggle on landing page reflects correct yearly amounts ($182 Pro / $470 Team)

### Alerting Channels
- [ ] `P0` Email alerts fire on missed/failed cron (Resend SMTP configured in app `.env`)
- [ ] `P1` Slack webhook alert channel works end-to-end (send test alert, confirm delivery)
- [ ] `P1` Webhook alert channel works (POST payload reaches configured URL)
- [ ] `P2` PagerDuty integration works for Pro/Team plans
- [ ] `P2` Free tier correctly blocked from all alert channels; upgrade prompt shown

---

## 2. Package Distribution

### Packagist — `crontinel/php`
- [ ] `P0` `crontinel/php` submitted to Packagist at `https://packagist.org/packages/crontinel/php`
- [ ] `P0` Stable tag `v0.1.0` pushed to `crontinel/php` GitHub repo so Packagist registers a stable version
- [ ] `P0` GitHub webhook installed in `crontinel/php` repo → Packagist (URL: `https://packagist.org/api/github?username=<packagist-user>`, events: push)
- [ ] `P0` `composer require crontinel/php` succeeds in a clean Laravel project with default `minimum-stability: stable`

### Packagist — `crontinel/laravel`
- [ ] `P0` `"crontinel/php": "@dev"` replaced with `"crontinel/php": "^0.1.0"` in `oss/composer.json`
- [ ] `P0` `repositories` path-repo block removed from `oss/composer.json`
- [ ] `P0` `oss/composer.lock` updated and committed after constraint change
- [ ] `P0` `crontinel/laravel` tagged `v0.3.0` and pushed; Packagist shows new tag within 1 minute
- [ ] `P0` `composer require crontinel/laravel` succeeds in a clean Laravel project (smoke test per RELEASE.md)
- [ ] `P1` Packagist webhook in `crontinel/crontinel` repo still valid after GitHub org move (token not rotated)
- [ ] `P1` GitHub badges in OSS README point to the correct repo (`crontinel/crontinel`, not `crontinel/laravel`)
- [ ] `P1` `crontinel/php` and `crontinel/laravel` repos are both public in the `crontinel` GitHub org

### npm — `@crontinel/mcp-server`
- [ ] `P1` `@crontinel` npm org exists; account is a member (`npm org ls crontinel`)
- [ ] `P1` `npm version 0.1.0` run in `mcp-server/`; `npm publish --access public` succeeds
- [ ] `P1` `npm view @crontinel/mcp-server version` returns `0.1.0`
- [ ] `P1` `npx @crontinel/mcp-server --help` (or `npx -y @crontinel/mcp-server`) runs without error
- [ ] `P2` Git commit + tag from `npm version` pushed to `crontinel/mcp-server` remote

---

## 3. Landing / Waitlist

### Waitlist Capture
- [ ] `P0` `RESEND_API_KEY` and `RESEND_AUDIENCE_ID` set in Cloudflare Pages → `crontinel-landing` → Settings → Environment Variables → Production
- [ ] `P0` Resend domain `crontinel.com` verified under Resend dashboard → Domains
- [ ] `P0` "Crontinel Waitlist" audience created in Resend; Audience ID matches env var
- [ ] `P0` Smoke test passes: fresh email submitted on `crontinel.com` appears as contact in Resend audience within 30 seconds
- [ ] `P0` `subscribe.ts` returns HTTP 503 with `{ unavailable: true }` when env vars are missing (stop silent fake-success — see WAITLIST_FALLBACK.md)

### Fallback
- [ ] `P1` Tally.so (or equivalent) fallback form created and URL ready to embed in the `unavailable` error state
- [ ] `P1` Client-side `index.astro` submit handler detects `unavailable: true` and shows amber fallback message with Tally link
- [ ] `P1` Any emails captured via fallback form imported into Resend audience once real keys are live

### Copy / UX
- [ ] `P1` "Docs" link added to landing page nav (links to `docs.crontinel.com`)
- [ ] `P1` Copy-to-clipboard buttons on install commands shown in landing page hero
- [ ] `P1` OSS vs. SaaS distinction is explained clearly on the landing page (what the SaaS adds over self-hosted)
- [ ] `P1` GitHub links in hero/OSS callout resolve to the correct repo (`crontinel/crontinel`, not `crontinel/laravel`)
- [ ] `P2` Rate limiting or Cloudflare Turnstile added to `/api/subscribe` before any public traffic
- [ ] `P2` `www.crontinel.com` redirect behavior confirmed (redirect to root or identical content — pick one)

---

## 4. Docs

### Quick-Start Accuracy
- [ ] `P0` Quick-start step 3 ("Run migrations") removed or corrected to note that `crontinel:install` runs migrations automatically — no manual `php artisan migrate` needed
- [ ] `P0` Quick-start step 4 (visit `/crontinel`) includes a "you should see X" screenshot or description of the empty-state dashboard
- [ ] `P1` Quick-start includes `php artisan schedule:run` as a required step for cron monitoring to produce data
- [ ] `P1` Quick-start includes a note: "Not using Horizon? Set `horizon.enabled = false` in `config/crontinel.php`"

### Docs Deployment
- [ ] `P0` Cloudflare Pages project created for `docs/` repo with build command `npm run build`, output `dist`, custom domain `docs.crontinel.com`
- [ ] `P0` `docs.crontinel.com` resolves and returns HTTP 200 (DNS auto-created by CF Pages custom domain)
- [ ] `P1` All internal docs links verified working (no broken anchors or dead pages)

### OSS README
- [ ] `P1` README documents that `crontinel:install` publishes config AND runs migrations automatically
- [ ] `P0` README install steps match the actual stable Packagist release (not `@dev`)

### Self-Hosting Guide
- [ ] `P1` Self-hosting guide (OSS) explains the full standalone install: package + local dashboard at `/crontinel`
- [ ] `P1` Self-hosting guide clarifies that the SaaS connection is optional

### MCP Guide
- [ ] `P1` MCP server guide published to `docs.crontinel.com` covering: install via `npx @crontinel/mcp-server`, Claude Code / Cursor config, what data is available
- [ ] `P2` MCP guide notes that API key requires Pro+ plan (Free tier is blocked)

---

## 5. Onboarding

### Registration
- [ ] `P0` `app.crontinel.com` DNS A record created pointing to Hetzner VPS IP (currently missing — DNS_AUDIT.md)
- [ ] `P0` Hetzner CX22 VPS provisioned per `app/docs/server-setup.md`; SSL cert issued via certbot
- [ ] `P0` Registration at `app.crontinel.com/register` loads and submits successfully
- [ ] `P0` Confirmation email sent on registration (Resend SMTP configured in app `.env`)

### Onboarding Wizard
- [ ] `P0` Timezone select in `onboarding/app.blade.php` replaced with `timezone_identifiers_list()` (matches `apps/create.blade.php`); search/filter added for usability
- [ ] `P0` API key field in onboarding step 3 has a copy-to-clipboard button
- [ ] `P0` Install commands in onboarding step 3 have copy-to-clipboard buttons
- [ ] `P1` "Test connection" button added to onboarding step 3; button calls `/api/ping` and shows "Connected! We received data from your app." confirmation
- [ ] `P1` Onboarding wizard visual matches the dark slate app theme (not Breeze default light)

### First Monitor Setup
- [ ] `P0` `composer require crontinel/laravel` succeeds after stable `crontinel/php` release (blocked by section 2)
- [ ] `P0` `php artisan crontinel:install` completes without errors on a fresh Laravel app
- [ ] `P0` After adding `CRONTINEL_API_KEY` to `.env` and running `php artisan schedule:run`, a ping appears in the SaaS dashboard within 60 seconds
- [ ] `P1` Livewire dashboard poll (`wire:poll.30000ms`) shows data after first successful ping without a manual page reload

---

## 6. Alerts / Integrations

### Working (to verify before launch)
- [ ] `P0` **Email** — Resend SMTP, `hello@crontinel.com` from address, verified domain; test alert delivers to inbox
- [ ] `P1` **Slack** — webhook URL stored per-monitor; test alert posts to correct channel
- [ ] `P1` **Webhook** — POST payload (JSON) delivered to user-configured URL; retry logic on failure
- [ ] `P2` **PagerDuty** — integration key configured; test incident creates and resolves in PagerDuty

### Planned / Not Yet Live
- [ ] `P2` **SMS** — not in current feature set; note as "coming soon" in docs if referenced on landing
- [ ] `P2` **OpsGenie / VictorOps** — document as future roadmap, not launch blockers

### Alert Gating
- [ ] `P1` Free tier: all alert channels blocked in UI, upgrade prompt shown with "Alerts require Pro" copy
- [ ] `P1` Pro tier: Slack, email, PagerDuty, webhook all enabled and accessible
- [ ] `P1` Team tier: all Pro channels plus custom alert rules (e.g., alert only after 3 consecutive failures)

---

## 7. Credibility / Trust Signals

### OSS / GitHub
- [ ] `P1` `crontinel/crontinel` GitHub repo is public with a complete README (install, config, alerts, screenshots)
- [ ] `P1` OSS repo has at least one stable tagged release (`v0.3.0`) visible on the releases page
- [ ] `P2` OSS repo has CI badge in README pointing to a green CI run

### Landing Page Trust
- [ ] `P1` "Open source" / "self-host for free" callout on landing links to the correct public GitHub repo
- [ ] `P1` Pricing page FAQ answers: "Is there a free tier?", "Can I self-host?", "Is my data safe?", "How do I cancel?"
- [ ] `P2` Testimonial or "used by X developers" social proof added once first users are onboarded (placeholder if none yet)
- [ ] `P2` Security/privacy policy page live at `crontinel.com/privacy` before collecting any emails or user data

### Status / Uptime
- [ ] `P1` `status.crontinel.com` live (Gatus deployed on Hetzner VPS, DNS A record added) — currently missing per DNS_AUDIT.md
- [ ] `P1` Status page monitors: `crontinel.com`, `app.crontinel.com`, `docs.crontinel.com`, ingest API endpoint
- [ ] `P2` Status page linked from landing page footer

### Billing Trust
- [ ] `P1` Stripe test mode confirmed off before first real transaction; live keys in production `.env`
- [ ] `P1` Invoice/receipt email configured in Stripe (Cashier sends these automatically — verify in Stripe dashboard)

---

## 8. Launch / Outreach Prep

### Infrastructure Readiness
- [ ] `P0` All P0 items in sections 1–7 complete
- [ ] `P0` `app.crontinel.com` live and responding HTTPS (no curl errors)
- [ ] `P0` `docs.crontinel.com` live and responding HTTPS
- [ ] `P0` Horizon worker running under Supervisor (`supervisorctl status crontinel-horizon:*` shows RUNNING)
- [ ] `P0` MySQL daily backup cron configured to S3 or Hetzner Object Storage (currently not configured — server-setup.md section 21)

### GitHub Actions / Deploy
- [ ] `P1` `DEPLOY_HOST`, `DEPLOY_USER`, `DEPLOY_SSH_KEY` secrets set in `HarunRRayhan/crontinel-app` → Settings → Secrets
- [ ] `P1` `workflow_run` trigger in `.github/workflows/deploy.yml` uncommented; CI push to `main` auto-deploys to production
- [ ] `P1` One successful GitHub Actions deploy run verified end-to-end

### Reddit Warmup
- [ ] `P1` Reddit account karma sufficient for posting in r/laravel, r/selfhosted, r/webdev without hitting new-account restrictions
- [ ] `P1` Identified the 3–5 subreddits for launch post (r/laravel, r/php, r/selfhosted, r/devops, r/SideProject at minimum)
- [ ] `P1` At least 2–3 genuine non-promotional comments made in target subreddits in the week before launch
- [ ] `P1` Launch Reddit post drafted (no em dashes; reviewed by user before posting per memory rules)

### Show HN
- [ ] `P1` Show HN draft written: "Show HN: Crontinel — Laravel cron job monitoring with Composer package and MCP server"
- [ ] `P1` Show HN draft reviewed: explains OSS-vs-SaaS distinction, links to GitHub and landing page, mentions MCP differentiation
- [ ] `P2` Timed for a weekday morning (US Eastern) for maximum HN visibility

### Email List
- [ ] `P1` Resend waitlist audience exported and reviewed before launch day
- [ ] `P1` Launch announcement email drafted to waitlist: what it is, how to start, free tier CTA, docs link
- [ ] `P1` Test send of launch email to a personal address before broadcast
- [ ] `P2` "Thanks for joining the waitlist" auto-reply email configured in Resend for new signups

### Launch Post Drafts
- [ ] `P1` Product Hunt launch post drafted (tagline, description, first comment, gallery screenshots)
- [ ] `P2` Product Hunt launch scheduled with a Hunter if possible (increases visibility)
- [ ] `P2` Twitter/X launch thread drafted (3–5 tweets: problem, solution, install demo, OSS link, call to try)
- [ ] `P2` Dev.to or Hashnode launch post drafted: "How I built cron job monitoring into my Laravel apps in 5 minutes"

---

## Summary — P0 Blockers

These items must be resolved before any public launch:

1. `crontinel/php` released to Packagist with a stable tag — `composer require crontinel/laravel` will fail without it
2. Hetzner VPS provisioned + `app.crontinel.com` DNS record added — the app is unreachable without it
3. Waitlist form stops silently succeeding when Resend is not configured
4. Registration gate removed — all CTAs link to `/register`, not `/#waitlist`
5. Timezone select in onboarding replaced with the full PHP list — wrong timezone = false positive alerts from day one
6. Docs deployed to `docs.crontinel.com` — the domain does not resolve yet
7. Stripe Price IDs wired into `config/cashier.php` — billing cannot process without them
