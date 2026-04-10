# Free Status Page Strategy: Crontinel

**Date:** 2026-04-10
**Project:** Crontinel app (HarunRRayhan/crontinel-app)

---

## 1. The Free Status Page Offer

Every Crontinel user gets one free, publicly accessible status page the moment they sign up. No credit card required, no trial expiration. The goal is simple: make status pages so easy and free that every Laravel developer creates one, and every status page becomes a marketing channel for Crontinel.

**What's included on the free tier:**

| Feature | Free |
|---|---|
| Status pages | 1 |
| URL format | `crontinel.com/status/{slug}` (path-based) |
| Monitor frequency | Every 15 minutes |
| HTTP endpoints displayed | 1 |
| Viewers | Unlimited (public) |
| SSL | Included (automatic, path-based on crontinel.com) |
| Branding | "Monitored by Crontinel" footer badge with link |
| Data retention | 30 days |
| Visibility | Public only |
| Incident history | Shown on page |
| Embeddable badge | Yes (SVG uptime badge) |

This is intentionally generous. A solo developer running a single Laravel app gets a real, production-quality status page for free, forever.

---

## 2. Free vs Pro vs Team Comparison

| Feature | Free ($0) | Pro ($19/mo) | Team ($49/mo) |
|---|---|---|---|
| **Status pages** | 1 | 1 per app (up to 5) | Unlimited |
| **URL format** | `crontinel.com/status/{slug}` | `{slug}.status.crontinel.com` | `status.yourdomain.com` (custom domain) |
| **Monitor frequency** | 15-minute checks | 1-minute checks | 30-second checks |
| **Endpoints per page** | 1 | Unlimited | Unlimited |
| **Data retention** | 30 days | 90 days | 1 year |
| **Visibility options** | Public only | Public or password-protected | Public, password-protected, or IP-restricted |
| **"Monitored by Crontinel" badge** | Always shown | Removable | Removable |
| **Custom logo/colors** | No | Yes | Yes |
| **Incident management** | Manual only | Manual + auto-detect | Manual + auto-detect + custom rules |
| **Embeddable SVG badge** | Yes | Yes | Yes |
| **Embeddable JS widget** | No | Yes | Yes |
| **Scheduled maintenance windows** | No | Yes | Yes |
| **Subscriber notifications** | No | Email subscribers | Email + Slack + webhook subscribers |
| **SSL** | Included (path-based) | Included (wildcard cert) | Included (Let's Encrypt via Caddy) |

**Upgrade triggers built into the comparison:**

- Developers who want branded status pages (no Crontinel badge) must go Pro.
- Developers who need password protection or custom domains must go Pro or Team.
- Developers who need faster check intervals or more endpoints hit the free limits naturally.

---

## 3. Growth Strategy

### 3.1 Auto-Create During Onboarding

After a user creates their first app and their first monitor reports healthy, Crontinel prompts them to create a status page with pre-filled defaults:

1. Slug auto-generated from app name (e.g., `my-laravel-app`)
2. The healthy monitor is pre-selected as the displayed endpoint
3. One click to publish

This removes all friction. The user goes from signup to live status page in under 5 minutes.

### 3.2 "Share Your Status Page" Prompt

Once the status page is live and the first successful check completes, show a prompt:

> Your status page is live! Share it with your users:
> `https://crontinel.com/status/my-laravel-app`
> [Copy Link] [Tweet It] [Add to README]

The "Add to README" option provides a markdown snippet with the embeddable badge. This is the highest-leverage action because it puts the Crontinel brand directly into GitHub repositories.

### 3.3 Embeddable Badge and Widget

Every status page gets a free SVG badge endpoint:

```
https://crontinel.com/badge/{slug}.svg
```

This badge shows a colored dot (green/yellow/red) and the current uptime percentage. Developers embed this in their GitHub READMEs, documentation sites, and landing pages.

The embed snippet provided to users:

```html
<a href="https://crontinel.com/status/my-app">
  <img src="https://crontinel.com/badge/my-app.svg" alt="Uptime Status" />
</a>
```

Every badge click sends traffic to the status page, which shows the "Monitored by Crontinel" branding.

### 3.4 Every Free Page Is a Marketing Touchpoint

The "Monitored by Crontinel" footer badge on free status pages is the core viral mechanic. It is:

- Small and non-intrusive (similar to "Powered by Vercel" or "Built with Notion")
- Linked to `crontinel.com?utm_source=status_page&utm_medium=badge&utm_campaign=free_tier&utm_content={slug}`
- Visible to every person who views the status page

If a free user's status page gets 100 views per month, that is 100 branded impressions per month, per user, at zero cost to Crontinel.

### 3.5 Social Proof Counter

Status pages display a subtle line in the footer:

> "Join 1,200+ developers monitoring their Laravel apps with Crontinel"

This number updates automatically based on total registered users. It reinforces that Crontinel is the standard choice for Laravel monitoring.

### 3.6 Status Page SEO

Each status page is a publicly indexed webpage on `crontinel.com`. This means:

- Every free status page adds a new indexed page to the Crontinel domain
- Status pages naturally contain keywords: the app name, "status," "uptime," "monitoring"
- Internal links from status pages to crontinel.com pass domain authority
- Status pages that receive backlinks (from READMEs, docs, landing pages) boost the entire crontinel.com domain

At 1,000 free users with status pages, Crontinel has 1,000+ indexed pages, all linking back to the main site.

---

## 4. Adoption Flywheel

The free status page creates a self-reinforcing growth loop:

```
1. Developer signs up for free
        |
        v
2. Sets up monitors for their Laravel app
        |
        v
3. Creates a free status page (guided by onboarding wizard)
        |
        v
4. Shares status page URL with customers, team, or community
        |
        v
5. Customers/viewers see "Monitored by Crontinel" badge
        |
        v
6. Some viewers are developers; they sign up for their own free account
        |
        v
7. Original developer hits free tier limits:
   - Needs alerts (not available on free)
   - Needs more than 1 endpoint on status page
   - Needs faster than 15-minute checks
   - Needs more than 1 app
   - Needs password-protected status page
   - Wants to remove Crontinel branding
        |
        v
8. Upgrades to Pro ($19/mo)
        |
        v
9. Cycle repeats with each new signup from step 6
```

**Why this flywheel works:**

- **Zero friction entry:** Free forever, no credit card, instant status page.
- **Built-in distribution:** Every status page markets Crontinel to the developer's audience.
- **Natural upgrade pressure:** The free tier is useful enough to adopt but limited enough to outgrow. Alerts are the biggest upgrade trigger since free has none.
- **Developer-to-developer spread:** Status pages are shared with technical audiences who are likely to need monitoring themselves.
- **Compounding SEO:** More users means more indexed pages means more organic traffic means more users.

**Key metrics to track:**

- Free-to-paid conversion rate (target: 5-8%)
- Status pages created per signup (target: >60%)
- Badge clicks per month per status page
- Signups attributed to status page badge (UTM tracking)
- Average time from signup to Pro upgrade

---

## 5. Technical Implementation

### 5.1 URL Routing by Tier

| Tier | URL Pattern | SSL Approach |
|---|---|---|
| Free | `crontinel.com/status/{slug}` | Automatic (same domain) |
| Pro | `{slug}.status.crontinel.com` | Wildcard certificate (`*.status.crontinel.com`) |
| Team | `status.yourdomain.com` | Let's Encrypt via Caddy, auto-provisioned |

Free tier uses path-based routing on the main domain. This is the simplest approach and has the added benefit of keeping all status page traffic on `crontinel.com` for SEO purposes.

Pro tier uses wildcard subdomains. One wildcard certificate covers all Pro status pages. DNS is handled with a wildcard CNAME record pointing `*.status.crontinel.com` to the Crontinel app server.

Team tier uses custom domains. When a Team user configures `status.yourdomain.com`, they add a CNAME record pointing to `custom.crontinel.com`. Caddy handles automatic Let's Encrypt certificate provisioning and renewal.

### 5.2 Rendering

Status pages are server-rendered Blade views, as decided in PRODUCT_STATUS_PAGE.md. No JavaScript framework required. The page loads fast, is fully indexable by search engines, and works without JavaScript enabled.

The Blade template includes:

- Page title (app name or custom title on Pro+)
- List of monitored endpoints with current status (green/yellow/red dot)
- Uptime percentage for each endpoint (calculated from retention window)
- Incident history timeline
- "Monitored by Crontinel" footer (controlled by `status_pages.show_branding` boolean)

### 5.3 "Monitored by Crontinel" Badge

The badge is a small footer element rendered in the Blade template:

```html
@unless($statusPage->show_branding === false)
<footer class="mt-8 text-center text-sm text-gray-500">
  <a href="https://crontinel.com?utm_source=status_page&utm_medium=badge&utm_campaign=free_tier&utm_content={{ $statusPage->slug }}"
     target="_blank"
     rel="noopener"
     class="inline-flex items-center gap-1 hover:text-gray-700">
    <svg><!-- Crontinel logo icon --></svg>
    Monitored by Crontinel
  </a>
</footer>
@endunless
```

The `show_branding` column defaults to `true`. Pro and Team users can set it to `false` from their status page settings. Free users cannot change this value.

### 5.4 Embeddable SVG Badge Endpoint

Route: `GET /badge/{slug}.svg`

The endpoint returns an SVG image with appropriate cache headers (cache for 5 minutes). The SVG displays:

- A colored circle: green (>99.5%), yellow (>95%), red (<95%)
- Text showing the uptime percentage: "99.9% uptime"

Response headers:

```
Content-Type: image/svg+xml
Cache-Control: public, max-age=300
```

This endpoint is rate-limited per IP (60 requests per minute) to prevent abuse.

### 5.5 Auto-Create on Signup Flow

The auto-creation flow triggers after the first monitor reports a successful check:

1. `MonitorCheckedSuccessfully` event fires
2. Listener checks if the user has zero status pages
3. If zero, create a status page with defaults:
   - `slug`: slugified app name
   - `is_public`: true
   - `show_branding`: true
   - Attach the triggering monitor to the status page
4. Flash a notification: "Your status page is ready! Share it with your users."
5. Show the share prompt with copy link, tweet, and README badge options

This only triggers once (when the user has zero status pages). It does not auto-create additional pages.

### 5.6 Database Changes

The three tables from PRODUCT_STATUS_PAGE.md remain as designed. One addition:

Add `show_branding` boolean to the `status_pages` table (default: `true`).

The middleware that serves status pages needs to check the tier:

- Free: enforce `show_branding = true`, enforce public visibility, enforce 1 endpoint limit
- Pro: allow `show_branding` toggle, allow password protection, allow unlimited endpoints
- Team: all Pro features plus custom domain support

---

## 6. Badge and Widget Design

### 6.1 SVG Uptime Badge

Format follows the shields.io convention that developers already recognize:

```
┌─────────────────────────────┐
│ ● uptime │ 99.9%           │
│ (green)  │ (white on green) │
└─────────────────────────────┘
```

Three states:

| Uptime | Dot Color | Background |
|---|---|---|
| > 99.5% | Green (#22c55e) | Green (#16a34a) |
| 95% to 99.5% | Yellow (#eab308) | Yellow (#ca8a04) |
| < 95% | Red (#ef4444) | Red (#dc2626) |

The badge links to the full status page. Clicking it takes the viewer to `crontinel.com/status/{slug}`.

### 6.2 HTML Embed Snippet

Provided to users in their status page settings:

```html
<a href="https://crontinel.com/status/my-app" target="_blank" rel="noopener">
  <img src="https://crontinel.com/badge/my-app.svg" alt="Uptime Status" />
</a>
```

### 6.3 Markdown Embed Snippet

For GitHub READMEs:

```markdown
[![Uptime Status](https://crontinel.com/badge/my-app.svg)](https://crontinel.com/status/my-app)
```

### 6.4 JavaScript Widget (Pro+ Only)

A lightweight script that renders a mini status overview:

```html
<div id="crontinel-status"></div>
<script src="https://crontinel.com/widget/{slug}.js" async></script>
```

The widget displays:

- 3 to 4 monitored endpoints with colored status dots
- Current uptime percentage for each
- "View full status" link to the status page
- Optional "Monitored by Crontinel" branding (shown on Pro unless disabled)

The widget JS is under 5KB gzipped. It fetches data from a JSON API endpoint (`/api/status/{slug}`) and renders a simple HTML block. No framework dependencies.

---

## 7. Updates to Existing Documents

### PRODUCT_STATUS_PAGE.md

The following sections need updating:

1. **Database schema:** Add `show_branding` boolean (default `true`) to the `status_pages` table.
2. **URL routing:** Document the three-tier URL strategy (path-based for free, subdomain for Pro, custom domain for Team). The current document only covers path-based for MVP.
3. **Blade template:** Add the "Monitored by Crontinel" footer component with conditional rendering.
4. **New route:** Add the `/badge/{slug}.svg` endpoint for embeddable badges.
5. **New route:** Add the `/widget/{slug}.js` endpoint for the Pro+ JavaScript widget.
6. **New route:** Add the `/api/status/{slug}` JSON endpoint for widget data.

### Pricing Page / Documentation

1. **Free tier description:** Update to mention "1 free status page" as a headline feature.
2. **Pro tier description:** Add "removable branding, password protection, subdomain URLs" to the status page section.
3. **Team tier description:** Add "custom domain status pages" to the feature list.
4. **Feature comparison table:** Add a "Status Pages" section with all the rows from the comparison table in section 2 above.

### Onboarding Flow

1. **Post-first-monitor step:** Add the auto-create status page prompt.
2. **Share prompt:** Add the "Share your status page" step with copy link, tweet, and README badge options.
3. **Dashboard:** Add a status page card/widget showing the page URL and view count.
