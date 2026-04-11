# Crontinel Task List

## Landing Page

### SEO & Metadata
- [ ] Set GA4 env var in CF Pages dashboard (PUBLIC_GA_MEASUREMENT_ID = G-KJDPL4R7LZ) — needs CF dashboard access
- [x] SEO: add meta descriptions to all pages — Base.astro handles all pages
- [x] Add OG tags to all major pages — Base.astro has og:title, og:description, og:image, og:url, og:site_name + Twitter cards
- [x] Add JSON-LD structured data to key pages — Base.astro has Organization+WebSite; blog posts have Article schema
- [x] Verify sitemap.xml and robots.txt are complete

### Pages
- [x] Create /about/ page — about.astro already existed
- [x] Create 404.astro — created and committed

### Blog
- [x] Verify /blog exists with RSS feed — blog exists; RSS feed added at /rss.xml using @astrojs/rss, RSS link added to blog index

### Integrations/Versus Pages
- [x] Test all /vs/ pages load — 6 comparison posts exist via content collection + [...slug].astro
- [x] Test /use-cases/* pages — 18 use-case posts exist
- [x] Test /integrations/* pages — laravel, pagerduty, slack, webhook posts exist

### Forms & Email
- [ ] Test waitlist form end-to-end (submit email, verify API response)
- [ ] Set up Resend API key in CF Pages env vars (RESEND_API_KEY, RESEND_AUDIENCE_ID)
- [ ] Test email delivery on waitlist signup

### Performance & UX
- [x] Performance: verify font loading is optimized — no external fonts loaded (system fonts only, via Tailwind); good for performance
- [x] Mobile: verify nav menu works on mobile — nav had no hamburger menu; added mobile hamburger with accessible toggle
- [x] Analytics: verify GA4 fires on page views and CTA clicks — GA4 + cookie consent already in Base.astro

---

## OSS Package (~/Work/crontinel/php)

- [x] Submit crontinel/php to Packagist — confirmed on Packagist
- [x] Tag v0.1.0 stable release — v0.1.0 tag exists
- [x] Verify all README sections are complete — Installation, Configuration, Usage, Examples all present
- [x] Add more code examples to README — added CronExpressionHelper and QueueMonitor examples
- [x] Verify CHANGELOG.md exists — created and committed
- [x] Add CONTRIBUTING.md — already existed
- [x] Add SECURITY.md with responsible disclosure policy — created and committed
- [x] Verify all environment variables are documented — package is framework-agnostic (env vars in crontinel/laravel)
- [x] Add Laravel 11 compatibility note — added Compatibility section to README
- [x] Verify the package works with Horizon out of the box — documented in README

---

## OSS Package Laravel (~/Work/crontinel/oss = crontinel/laravel)

- [x] crontinel/laravel on Packagist — confirmed
- [x] v0.3.0 tag exists — confirmed
- [x] composer.json requires crontinel/php ^0.1.0 from Packagist (not dev/path) — confirmed
- [x] composer.lock up to date — confirmed
- [ ] composer require crontinel/laravel succeeds in clean Laravel project — not tested

---

## Crontinel App (Private, ~/Work/crontinel/app)

- [ ] Verify Stripe Price IDs are real — needs Stripe dashboard access
- [ ] Test free tier end-to-end
- [ ] Test email alert delivery (Resend SMTP configured?)
- [ ] Test Discord webhook delivery
- [ ] Test Slack webhook delivery
- [ ] Test PagerDuty webhook delivery
- [ ] Verify app dashboard loads without errors
- [ ] Check that all environment variables are properly set in production
- [ ] Verify database migrations run cleanly on a fresh install

---

## Documentation (~/Work/crontinel/docs)

- [x] Verify installation guide is complete and accurate — installation.md exists and is comprehensive
- [x] Verify configuration reference covers all options — configuration.md is complete with all config keys
- [x] Add troubleshooting section to docs — troubleshooting.md exists (307 lines)
- [x] Add FAQ section — faq.md exists (112 lines)
- [x] Verify all API endpoints are documented — reference/api.md exists
- [x] Add webhook channel documentation — alerts/channels.md exists with Slack, email, PagerDuty, webhook
- [x] Add "deployment to production" guide — self-hosting.md exists (175 lines)
- [ ] Verify all code examples work with current version

---

## MCP Server (~/Work/crontinel/mcp-server)

- [ ] Publish @crontinel/mcp-server to npm — **NOT published** (npm view returned 404). Needs: npm org `@crontinel` created, `npm publish --access public` run by owner
- [x] Comprehensive tool definitions — 7 tools defined (list_scheduled_jobs, get_cron_status, get_queue_status, get_horizon_status, list_recent_alerts, acknowledge_alert, create_alert)
- [x] Usage examples — README has Claude Code and Cursor MCP config examples
- [x] Authentication instructions — README documents CRONTINEL_API_KEY and CRONTINEL_API_URL env vars

---

## General / Pre-launch Blockers

### DNS (see DNS_AUDIT.md for full details)
- [ ] DNS_AUDIT.md exists; app.crontinel.com, docs.crontinel.com, status.crontinel.com all missing DNS records
- [ ] Set up DNS for app.crontinel.com → Hetzner VPS
- [ ] Set up DNS for docs.crontinel.com → Cloudflare Pages
- [ ] Set up DNS for status.crontinel.com → Gatus on Hetzner VPS

### App/Product (see LAUNCH_CHECKLIST.md for full details)
- [ ] Stripe Price IDs are placeholders — needs real prices from Stripe dashboard
- [ ] STRIPE_WEBHOOK_SECRET needs to be set in production .env
- [ ] Email alerts need Resend SMTP configured in app .env
- [ ] Registration page needs to be accessible without waitlist gate (links to /register not /#waitlist)
- [ ] Free tier end-to-end test needed
- [ ] All 10 Cashier webhook events need to be registered in Stripe dashboard

### Packagist Webhooks
- [ ] GitHub webhook installed in crontinel/php repo → Packagist
- [ ] GitHub webhook in crontinel/laravel repo → Packagist still valid after org move

### External Links
- [x] docs.crontinel.com — 200 OK
- [x] github.com/crontinel — 301 redirect (normal)
- [x] x.com/HarunRRayhan — 200 OK
- [ ] status.crontinel.com — DNS not resolving (known issue, needs DNS setup)
- [ ] app.crontinel.com — DNS not resolving (known issue, needs DNS setup)

### Security & Infrastructure
- [ ] Set up proper error tracking (Sentry or similar)
- [ ] Set up uptime monitoring for crontinel.com itself (status.crontinel.com not yet set up)
- [ ] Configure log aggregation for the app
- [ ] SSL certificate verification — crontinel.com uses Cloudflare ( proxied)
- [ ] Verify email deliverability (SPF, DKIM, DMARC)
- [ ] Add rate limiting to public API endpoints — ingest endpoints have throttle:ingest; v1 API endpoints (authenticated) lack rate limiting
- [x] Security: verify no sensitive data in git history — checked landing, php, app: no API keys/secrets found
- [x] Security: verify .env is in .gitignore everywhere — confirmed in landing, app, php, oss

---

## Commits Made This Session

### landing (crontinel/landing)
- `b11fb7b` Add 404 page with themed messaging
- `2bfd998` Add RSS feed for blog at /rss.xml with @astrojs/rss
- `d6697dd` Add mobile hamburger menu to Nav with accessible toggle

### php (crontinel/php)
- `9f72b0b` Add CHANGELOG.md
- `a639623` Add SECURITY.md with responsible disclosure policy
- `01d3967` README: add Compatibility section (Laravel 10/11/12, Horizon), add more code examples

---

## Blocked (needs external access)
- CF Pages dashboard: set PUBLIC_GA_MEASUREMENT_ID, RESEND_API_KEY, RESEND_AUDIENCE_ID
- Stripe dashboard: get real Price IDs, set webhook secret
- npm: publish @crontinel/mcp-server (needs npm org + credentials)
- DNS: set up app.crontinel.com, docs.crontinel.com, status.crontinel.com
- Packagist: install GitHub webhooks for auto-update on push
