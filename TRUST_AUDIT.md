# Crontinel Trust-Signal Audit

Date: 2026-04-08

---

## 1. Trust-Gap Report

### P0 — Launch Blockers

| # | Gap | Where | Notes |
|---|-----|-------|-------|
| 1 | **Zero screenshots anywhere** | All repos, landing, docs | No real dashboard screenshot exists. Landing has an HTML mockup. Docs have no images at all. OSS README has zero visuals. A developer evaluating the tool cannot see what they are installing. |
| 2 | **No demo or video** | Landing, docs | No live demo, no 60-second install video, no GIF showing the dashboard in action. Competitors (Cronitor, Better Stack) all have these. |
| 3 | **LICENSE file missing from 6 of 7 repos** | app, docs, hub, landing, mcp-server, php | Only `oss/` has a CHANGELOG. No repo has a LICENSE file on disk. The OSS README says "MIT" but there is no LICENSE file to back it. GitHub shows "No license" for repos without one, which is a red flag for developers evaluating OSS. |
| 4 | **No CHANGELOG except oss/** | app, docs, hub, landing, mcp-server, php | Only `oss/CHANGELOG.md` exists. Landing has a `/changelog` page with one entry ("Crontinel is live"). No versioned history anywhere else. |
| 5 | **Docs have no verification screenshots** | docs quick-start | After "Visit /crontinel in your browser" there is no image showing what the user should see. No confirmation they succeeded. |
| 6 | **Quick-start missing scheduler prerequisite** | docs/quick-start.md | Cron monitoring depends on `schedule:run` being in crontab. Quick-start never mentions this. User installs, sees empty cron section, thinks it is broken. |

### P1 — Launch-Week Musts

| # | Gap | Where | Notes |
|---|-----|-------|-------|
| 7 | **No docs link in landing page nav** | landing Nav.astro | The docs site (docs.crontinel.com) is never linked above the fold. Evaluating developers cannot find technical documentation from the marketing site without scrolling to the footer or guessing the URL. |
| 8 | **CONTRIBUTING.md missing from all public repos** | oss, php, mcp-server, hub | OSS projects without a CONTRIBUTING file signal "we don't want contributions," which undermines community trust. |
| 9 | **No CI badge on php or mcp-server** | php README, mcp-server README | `oss/` has CI + Packagist + downloads badges. `php/` has version + PHP + license but no CI. `mcp-server/` has no badges at all. Inconsistent badge presence across ecosystem repos looks unfinished. |
| 10 | **hub repo has no badges or install instructions** | hub README | The meta-hub README is a plain link index. It should be the "front door" for the GitHub org. No badges, no quick install snippet at the top. |
| 11 | **Landing changelog has one entry** | landing/changelog.astro | Single "Crontinel is live" entry. A thin changelog signals the project is brand new and untested. |
| 12 | **No "copy to clipboard" on install commands** | Landing hero, docs quick-start | The `composer require crontinel/laravel` is shown as passive text. No copy button. Small friction, but it signals polish. |
| 13 | **Quick-start has no "not using Horizon" note** | docs/quick-start.md | Users without Horizon will see an empty Horizon section and think something broke. The OSS README has this note; the docs do not. |
| 14 | **php and mcp-server repos have no CI workflows** | .github/workflows/ | No automated tests visible to the public. CI badges cannot be shown because CI does not exist. |

### P2 — Pre-Launch Nice-to-Haves

| # | Gap | Where | Notes |
|---|-----|-------|-------|
| 15 | **No social proof of any kind** | Landing page | No GitHub star count, no "used by" logos, no testimonial placeholders, no download count callout. Page has zero external validation signals. |
| 16 | **No comparison table on landing page** | Landing (vs/ pages exist but are separate) | The `/vs/cronitor`, `/vs/better-stack` etc. pages exist but the homepage has no quick feature comparison. Competitors do this above the fold. |
| 17 | **No "Built by" / founder credibility section** | Landing page | No about section, no author photo, no link to the builder's profile. For a pre-traction product, founder identity is a major trust signal. |
| 18 | **No status page or uptime badge for the SaaS** | Landing, app | No public status page (e.g., status.crontinel.com). Ironic for a monitoring product. |
| 19 | **Blog is empty** | landing/blog/ | Blog index page exists but has no posts. An empty blog is worse than no blog link at all. |
| 20 | **Ecosystem table links inconsistent** | Various READMEs | Some READMEs link to `github.com/crontinel/crontinel`, others to `github.com/HarunRRayhan/crontinel-app`. URLs should all use the public-facing org paths once repos are transferred. |

---

## 2. Top 5 Highest-Value Fixes Before Launch

### 1. Add real dashboard screenshots to OSS README, docs, and landing page

**Why:** A developer deciding whether to install a package looks at the README first. A package with no screenshots gets skipped. The landing page HTML mockup is decent but a real screenshot proves the product exists.

**What to do:**
- Take 3 screenshots: (a) the local `/crontinel` dashboard with sample data, (b) the SaaS multi-app view, (c) an alert firing in Slack.
- Add the dashboard screenshot to the OSS README right below "Visit /crontinel in your browser."
- Add it to docs/quick-start.md as the "you should see this" verification step.
- Replace or supplement the HTML mockup on the landing page with the real screenshot.

**Effort:** 1-2 hours (seed sample data, take screenshots, add to markdown/astro files).

**Can be done today:** Yes, using local dev with seeded data.

### 2. Add LICENSE files to all public repos

**Why:** GitHub shows "No license" prominently on repo pages. For an OSS project claiming MIT, this is a trust destroyer. Developers will not install a package with no license file, period.

**What to do:**
- Add a standard MIT LICENSE file (with "Harun R Rayhan" and 2026 year) to: oss, php, mcp-server, hub, docs, landing.
- The app repo can use a proprietary notice or skip it (it is private).

**Effort:** 15 minutes.

**Can be done today:** Yes.

### 3. Add the scheduler prerequisite and a verification step to the quick-start

**Why:** Without `schedule:run` in crontab, the cron monitor produces zero data. A user who follows the quick-start exactly will see an empty cron section and think the product is broken. This is the most likely first-run failure mode.

**What to do:**
- Add a step between current steps 3 and 4: "Make sure Laravel's scheduler is running" with the crontab line.
- Add a note after step 4: "Not using Horizon? Set `horizon.enabled = false` in `config/crontinel.php` to hide the Horizon section."
- Add a "You should see" description (or screenshot) after "Visit /crontinel."

**Effort:** 30 minutes.

**Can be done today:** Yes.

### 4. Seed the changelog with real entries and add a "Built by" section to the landing page

**Why:** A single-entry changelog and an anonymous product both signal "this might disappear tomorrow." Early users need to trust the builder and see active development.

**What to do:**
- Port the `oss/CHANGELOG.md` entries (0.1.0 and 0.2.0) to the landing `/changelog` page with proper formatting.
- Add a brief "Built by" or "About" section to the landing page footer area: name, photo, GitHub link, one sentence ("I'm Harun, a Laravel developer building the monitoring tool I wanted to exist").
- Optionally add a GitHub star button/count to the OSS callout section on the landing page.

**Effort:** 1-2 hours.

**Can be done today:** Yes.

### 5. Add CI workflows and badges to php and mcp-server repos

**Why:** Public repos without CI look unmaintained. The OSS repo has good badges (version, CI, downloads, PHP, Laravel, license). The php and mcp-server repos should match.

**What to do:**
- Add a basic CI workflow to `php/` (run tests on push, PHP 8.2/8.3/8.4 matrix).
- Add a basic CI workflow to `mcp-server/` (lint + test on push).
- Add badge rows to both READMEs matching the OSS repo pattern.

**Effort:** 1-2 hours.

**Can be done today:** Yes.

---

## 3. Today vs Needs Product Live

### Can be done today (no live product required)

| Fix | Effort |
|-----|--------|
| Add LICENSE files to all repos | 15 min |
| Add screenshots using local dev with seed data | 1-2 hr |
| Fix quick-start (scheduler step, verification, Horizon note) | 30 min |
| Port changelog entries to landing page | 30 min |
| Add "Built by" section to landing footer | 30 min |
| Add CI workflows to php and mcp-server | 1-2 hr |
| Add CONTRIBUTING.md to OSS repos | 30 min |
| Add docs link to landing Nav | 10 min |
| Normalize ecosystem table URLs across READMEs | 30 min |
| Add badges to php and mcp-server READMEs | 15 min |
| Remove or hide empty blog link (or write one launch post) | 30 min |

### Needs product to be live first

| Fix | Why |
|-----|-----|
| GitHub star count widget on landing | Need real stars to display |
| "Used at X companies" social proof | Need real users |
| Testimonials section | Need real users |
| Packagist download count callout | Need real installs |
| Public status page (status.crontinel.com) | Need the SaaS running in production |
| Real user data in SaaS dashboard screenshot | Can fake with seed data now; real data comes later |
| Blog posts about real production incidents caught by Crontinel | Need usage stories |

### Things you can fake/seed now as placeholders

| Signal | How |
|--------|-----|
| **GitHub star count** | Add a "Star us on GitHub" button (links to repo). Even 0 stars with a button looks intentional. |
| **Download count** | Once on Packagist, the badge auto-updates. Seed a few `composer require` from different machines to get it off zero. |
| **Changelog depth** | You already have two solid releases (0.1.0, 0.2.0). Port them to the landing page changelog and they instantly make the project look active. |
| **Community signals** | Enable GitHub Discussions on the hub repo (already linked in hub README). An empty but enabled Discussions tab is better than no community channel. |
| **"Open source" trust badge** | Add an "MIT Licensed" badge or callout to the landing page hero area. OSS is a major trust signal for dev tools. |
