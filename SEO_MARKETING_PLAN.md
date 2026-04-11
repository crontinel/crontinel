# Crontinel SEO + Marketing Plan

Last updated: 2026-04-11

**Audience:** Laravel developers who self-host web apps and need to monitor Horizon queues, cron jobs, and background job health.

**Goal:** Become the default Laravel-native cron/queue monitoring tool within 12 months.

---

## Table of Contents

1. [Keyword Research](#1-keyword-research)
2. [On-Page SEO](#2-on-page-seo)
3. [Content Strategy](#3-content-strategy)
4. [Technical SEO](#4-technical-seo)
5. [Off-Page SEO](#5-off-page-seo)
6. [GSC Monitoring](#6-gsc-monitoring)
7. [Target Audience](#7-target-audience)
8. [Distribution Channels](#8-distribution-channels)
9. [Launch Strategy](#9-launch-strategy)
10. [Community Building](#10-community-building)
11. [Paid Channels](#11-paid-channels)
12. [KPIs to Track](#12-kpis-to-track)
13. [30-Day Sprint Plan](#13-30-day-sprint-plan)

---

## 1. Keyword Research

### Strategy

Target three layers: informational (how-to content), transactional (tool comparisons/alternatives), and brand/comparison (vs. Cronitor, etc.). Laravel-specific keywords have lower competition and higher buyer intent than generic monitoring terms.

### Keyword Table

| # | Keyword | Monthly Volume (est.) | Search Intent | Competition | Priority |
|---|---|---|---|---|---|
| 1 | laravel cron job monitoring | 500-1K | Informational | Low | **HIGH** |
| 2 | monitor laravel horizon | 300-700 | Informational | Low | **HIGH** |
| 3 | laravel queue monitoring | 400-900 | Informational | Low | **HIGH** |
| 4 | laravel scheduled tasks not running | 200-500 | Informational | Low | **HIGH** |
| 5 | laravel cron job failed alert | 100-300 | Informational | Very Low | **HIGH** |
| 6 | laravel cron monitoring tool | 100-300 | Transactional | Low | **HIGH** |
| 7 | cron job monitoring saas | 300-700 | Transactional | Medium | **HIGH** |
| 8 | laravel horizon queue stuck | 200-500 | Informational | Low | **HIGH** |
| 9 | cronitor alternative | 200-400 | Transactional | Medium | **HIGH** |
| 10 | healthchecks.io alternative | 100-300 | Transactional | Low | **HIGH** |
| 11 | cron job monitoring open source | 200-500 | Informational | Medium | MED |
| 12 | laravel worker health check | 100-300 | Informational | Very Low | **HIGH** |
| 13 | background job monitoring php | 100-300 | Informational | Low | MED |
| 14 | laravel cron heartbeat | 100-200 | Informational | Very Low | **HIGH** |
| 15 | scheduled task monitoring self hosted | 100-200 | Informational/Trans. | Very Low | MED |
| 16 | best cron monitoring tool | 500-1K | Transactional | Medium | MED |
| 17 | crontinel vs cronitor | <100 | Brand | Very Low | MED |
| 18 | laravel horizon monitoring dashboard | 100-300 | Informational | Very Low | **HIGH** |
| 19 | php cron job missed alert | 100-200 | Informational | Very Low | MED |
| 20 | cron job downtime notification | 200-400 | Transactional | Low | MED |

### Keyword Clusters

**Cluster A: Laravel-specific (primary)** — target with docs, blog posts, landing page copy.
Keywords: 1, 2, 3, 4, 5, 6, 8, 12, 14, 18

**Cluster B: Tool comparisons (high-converting)** — target with dedicated comparison pages.
Keywords: 9, 10, 17

**Cluster C: Generic cron monitoring (volume play)** — target with blog content.
Keywords: 7, 11, 13, 15, 16, 19, 20

---

## 2. On-Page SEO

### Homepage (`crontinel.com`)

- **Title tag:** `Crontinel — Laravel Cron Job & Queue Monitoring | Never Miss a Failed Job`
- **Meta description:** `Monitor Laravel cron jobs, Horizon queues, and background workers. Get alerted in minutes when a scheduled task fails. Free tier. No agent to install.`
- **H1:** `Know when your cron jobs stop running — before your users do`
- **Target keywords:** laravel cron job monitoring, cron job monitoring SaaS, laravel queue monitoring
- **Checklist:**
  - [ ] H1 contains primary keyword naturally
  - [ ] Hero section mentions Laravel, Horizon, cron monitoring in first 100 words
  - [ ] Features section uses semantic keywords: "scheduled tasks," "background jobs," "queue workers," "heartbeat monitoring"
  - [ ] Comparison table targets [competitor] alternative searches
  - [ ] Social proof (GitHub stars, testimonials) above the fold
  - [ ] Schema: SoftwareApplication markup with price range
  - [ ] Internal links to /docs, /pricing, /blog from homepage
  - [ ] Page speed: LCP < 2.5s, no layout shift from font loading

### Pricing Page (`/pricing`)

- **Title tag:** `Crontinel Pricing — Free, Pro $19/mo, Team $49/mo`
- **Meta description:** `Start free with 5 monitors. Upgrade to Pro for unlimited monitors and alerts. Laravel-native cron and queue monitoring that fits your budget.`
- **H1:** `Simple pricing for serious monitoring`
- **Checklist:**
  - [ ] FAQ section targets "is Crontinel worth it," "Crontinel vs Cronitor pricing"
  - [ ] Structured data: FAQPage schema for pricing FAQ
  - [ ] "Free forever" tier is explicitly labeled (reduces bounce)
  - [ ] Annual/monthly toggle — both prices visible for SEO (use `<noscript>` fallback)
  - [ ] Comparison table vs. Cronitor and Healthchecks.io (structured with `<table>`)
  - [ ] CTA above fold: "Start free — no credit card"
  - [ ] Breadcrumb: Home > Pricing

### Docs Index (`/docs`)

- **Title tag:** `Crontinel Documentation — Laravel Cron & Horizon Monitoring`
- **Meta description:** `Complete documentation for Crontinel. Install via Composer, configure cron monitors, set up Horizon monitoring, and connect Slack alerts in minutes.`
- **H1:** `Crontinel Documentation`
- **Checklist:**
  - [ ] Quick-start link prominent and above fold
  - [ ] Installation section ranks for "composer require crontinel/laravel"
  - [ ] Each doc page has a unique title + meta
  - [ ] Code blocks indexed (Google crawls and indexes code snippets)
  - [ ] Breadcrumbs on every docs page
  - [ ] `sitemap.xml` includes all `/docs/*` URLs

### Blog (`/blog`)

- **Title tag:** `Crontinel Blog — Laravel Monitoring & DevOps`
- **Meta description:** `Practical guides on Laravel cron job monitoring, Horizon queue management, background job alerts, and PHP app reliability.`
- **Checklist:**
  - [ ] Category pages: `/blog/category/laravel`, `/blog/category/cron-monitoring`
  - [ ] Author schema on each post (improves E-E-A-T)
  - [ ] Related posts section links internally
  - [ ] Posts target one primary keyword each (see Content Strategy)
  - [ ] JSON-LD Article schema on each post
  - [ ] OG image generated per post (dynamic with post title)

---

## 3. Content Strategy

### Goal

Build topical authority around Laravel background job monitoring. Every post targets a real search query. Publish 1 post every 10-14 days at launch cadence.

### 12 Blog Post Topics

| # | Title | Primary Keyword | SEO Angle | Priority |
|---|---|---|---|---|
| 1 | **How to Monitor Laravel Horizon Queues in Production** | monitor laravel horizon | Comprehensive guide; targets "how to" featured snippet. Step-by-step with code. | **HIGH — publish first** |
| 2 | **Why Your Laravel Cron Jobs Fail Silently (And How to Fix It)** | laravel cron job failed alert | Pain-first content; solves real problem developers Google after an incident. | **HIGH** |
| 3 | **Laravel Scheduled Task Monitoring: The Complete Guide** | laravel cron job monitoring | Pillar post. Links to all other content. Targets the highest-volume keyword. | **HIGH** |
| 4 | **Cronitor vs Crontinel: Which is Better for Laravel?** | cronitor alternative | Comparison page that converts Cronitor searchers. Honest, not pure sales copy. | **HIGH** |
| 5 | **Healthchecks.io vs Crontinel: A Side-by-Side Comparison** | healthchecks.io alternative | Same playbook as above. Target OSS community considering paid options. | **HIGH** |
| 6 | **How to Get Slack Alerts When a Laravel Queue Worker Dies** | laravel worker health check | Tutorial that solves a specific, high-intent pain point. Ends with Crontinel CTA. | **HIGH** |
| 7 | **Setting Up Cron Job Monitoring for Self-Hosted Laravel Apps** | laravel cron monitoring tool | Targets self-hosters specifically; aligns with Crontinel's OSS/self-host angle. | MED |
| 8 | **How to Debug Laravel Horizon Queue Stuck Jobs** | laravel horizon queue stuck | Debug-focused; high-traffic query. Include Crontinel as part of the debugging toolkit. | MED |
| 9 | **The Real Cost of Unmonitored Cron Jobs in Production** | cron job monitoring SaaS | Business case content. Targets decision-makers who need to justify the $19/mo spend. | MED |
| 10 | **PHP Background Job Monitoring: Tools and Best Practices** | background job monitoring php | Broader PHP audience; Crontinel mentioned as Laravel-specific option. | MED |
| 11 | **How to Use Laravel's `withoutOverlapping()` and Monitor It** | laravel scheduled tasks not running | Niche tutorial; very low competition; targets a specific Laravel feature. | LOW |
| 12 | **Building a Cron Heartbeat System for Laravel: DIY vs SaaS** | cron job heartbeat | DIY builders vs. paid tools. Honest comparison; Crontinel wins on "time to value." | LOW |

### Content Rules

- Each post: 1,200-2,500 words minimum
- Include working code examples (Laravel-native)
- No AI-pattern writing: no "In conclusion," no em dashes, no "delve into"
- H2/H3 structure targets featured snippets for how-to queries
- End every post with a subtle CTA: "Crontinel monitors this automatically — free to start"
- Cross-link between posts (build topical clusters)

---

## 4. Technical SEO

### Core Web Vitals Targets

| Metric | Target | Current status |
|---|---|---|
| LCP (Largest Contentful Paint) | < 2.5s | Verify with PageSpeed Insights |
| INP (Interaction to Next Paint) | < 200ms | Verify with CrUX data |
| CLS (Cumulative Layout Shift) | < 0.1 | Watch for font loading shifts |
| TTFB | < 800ms | Cloudflare Pages handles this well |

### Sitemap

- Generate `sitemap.xml` from all routes automatically (Laravel package: `spatie/laravel-sitemap`)
- Include: homepage, /pricing, /blog, all /blog/*, all /docs/*
- Exclude: /dashboard, /settings, /api/*, /admin/*
- Submit to GSC immediately after launch
- Regenerate on every blog publish (can trigger from deploy webhook)

### robots.txt

```
User-agent: *
Allow: /
Disallow: /dashboard
Disallow: /settings
Disallow: /api/
Disallow: /admin/
Sitemap: https://crontinel.com/sitemap.xml
```

### Schema.org Setup

**Homepage:**
```json
{
  "@type": "SoftwareApplication",
  "name": "Crontinel",
  "applicationCategory": "DeveloperApplication",
  "operatingSystem": "Web",
  "offers": {
    "@type": "Offer",
    "price": "0",
    "priceCurrency": "USD"
  }
}
```

**Blog posts:** Article schema with author, datePublished, dateModified.

**Pricing page:** FAQPage schema for pricing questions.

**Docs pages:** BreadcrumbList schema.

### Additional Technical Checks

- [ ] Canonical tags on all pages (prevent duplicate content from pagination)
- [ ] `hreflang` not needed (English-only for now)
- [ ] 404 page is custom (not a framework default) and links back to homepage
- [ ] HTTPS enforced, no mixed content warnings
- [ ] No broken internal links (run Screaming Frog or Ahrefs audit monthly)
- [ ] Open Graph tags on all pages (title, description, image)
- [ ] Twitter Card meta tags
- [ ] No orphan pages (all content reachable from navigation or sitemap)

---

## 5. Off-Page SEO

### 6 Backlink Sources to Pursue

**1. Laravel News (laravel-news.com)**
Submit Crontinel as a tool/package. Laravel News has a packages section that links to new Composer packages. This is the highest-priority backlink for the Laravel audience. Submit via their "Submit a package" link. Aim for a full sponsored post ($199-499) if budget allows at launch.

**2. Packagist / GitHub**
The `crontinel/laravel` package on Packagist and the GitHub repo both rank in Google. Make sure the Packagist description includes keywords ("Laravel cron monitoring, Horizon queue health"). The GitHub README should be a full marketing document, not just a code reference.

**3. DEV.to Guest Posts**
Write 2-3 technical posts on DEV.to targeting Laravel developers. DEV.to articles rank well for developer queries. Each post links back to crontinel.com and the GitHub repo. Topics: "How I monitor Laravel Horizon with open-source tools" and "The cron job failure that cost me 3 days of debugging."

**4. Reddit r/laravel (community presence, not spam)**
Organic mentions when Crontinel is genuinely relevant in threads asking about monitoring. Each comment on Reddit that links back counts as a backlink (nofollow, but builds domain mentions). See Community Building section for rules.

**5. PHP/Laravel Directories and Tooling Lists**
Submit to: Laracasts community tools, Made With Laravel, AwesomeLaravel GitHub list, PHP Ranked. These are low-effort, permanent backlinks. Each directory submission takes 20 minutes.

**6. Spatie's Ecosystem (partner/mention play)**
Crontinel complements `spatie/laravel-schedule-monitor` and Oh Dear. Reach out to Spatie directly (Freek Van der Hagen on X/GitHub). Position Crontinel as a cloud monitoring companion to their OSS tool. If they mention Crontinel in their docs ("If you want cloud-hosted monitoring, check out Crontinel"), that's a high-authority backlink and credibility transfer.

### Guest Post Targets

| Target | Audience | Topic Angle |
|---|---|---|
| Laravel News | Laravel devs | "Building a Cron Monitor with Laravel: What I Learned" |
| DEV.to | PHP/Laravel devs | "Why Your Cron Jobs Are Silently Broken in Production" |
| Laracasts Blog | Laravel learners | "Setting Up Production Monitoring for Laravel Scheduled Tasks" |
| HackerNoon | Dev/engineering | "The Developer Tax of Unmonitored Background Jobs" |

### Directory Submissions

Submit to these directories within launch week:
- Product Hunt (launch day)
- Hacker News "Show HN"
- Made With Laravel (madewithlarvavel.com)
- Awesome Laravel (GitHub curated list)
- AlternativeTo.net (add Crontinel as alternative to Cronitor)
- SaaSHub.com (developer tool directory)
- StackShare (add as alternative to Cronitor, Better Stack)
- PHP Ranked

---

## 6. GSC Monitoring

### Weekly Checks (every Monday, 15 minutes)

1. **Performance > Search Results**
   - Filter last 28 days vs. previous 28 days
   - Watch: Total clicks, total impressions, average CTR, average position
   - Flag: Any page with impressions > 100 and CTR < 2% (title/meta needs work)

2. **Coverage > Errors**
   - Fix any 404 errors immediately (often broken internal links)
   - Fix any "Discovered but not indexed" pages (check robots.txt, canonical, noindex)
   - Fix any "Soft 404" (pages returning 200 but showing no content)

3. **Core Web Vitals**
   - Check URLs flagged as "Poor" LCP or CLS
   - Fix within 2 weeks of flagging

4. **Queries report**
   - Look for unexpected queries driving impressions (surface new blog post ideas)
   - Look for queries ranking position 5-15 (easy wins with content updates)

5. **Links report**
   - Review top linking sites monthly (ensure no toxic backlinks)
   - Track growth in referring domains

### Monthly Actions

- Pull top 10 queries by impressions, verify content is optimized for each
- Submit sitemap refresh after any batch of new pages
- Check for manual actions (should be none, but verify)

---

## 7. Target Audience

### Segment 1: Solo Laravel Developers

**Who:** Freelancers and indie developers running 1-5 Laravel apps in production. They are the only engineer for their projects.

**What they Google:**
- "laravel cron job not running"
- "how to know if laravel queue is down"
- "laravel horizon monitoring dashboard"

**Pain points:**
- Cron jobs fail silently; they find out from angry users, not from alerts
- No time to build custom monitoring
- Don't want to pay $50/mo for a full observability platform
- Horizon dashboard only works when they're logged in and actively looking

**Why Crontinel:** $19/mo with unlimited monitors is their ROI calculation — one hour of debugging time saved per month justifies the cost. Composer package means zero infrastructure overhead.

---

### Segment 2: Small Engineering Teams (2-8 developers)

**Who:** Early-stage SaaS companies with 2-8 engineers. Laravel is their primary stack. They have production jobs that run critical business logic (invoicing, notifications, reports).

**What they Google:**
- "laravel cron monitoring"
- "monitor laravel jobs production"
- "cronitor alternative"

**Pain points:**
- Jobs fail and nobody gets paged — they find out from a customer complaint
- Cronitor is getting expensive as they add monitors
- They need Slack alerts, not just email
- Horizon process crashes and restarts silently; jobs queue up for hours

**Why Crontinel:** Unlimited monitors on the Team plan ($49/mo) undercuts Cronitor at scale. Slack integration is native. Team plan is per-team, not per-seat.

---

### Segment 3: Agency Developers / Consultants

**Who:** Laravel agencies or freelancers managing multiple client apps. They run cron jobs across 5-20+ different projects.

**What they Google:**
- "monitor multiple laravel apps"
- "cron monitoring for multiple clients"
- "laravel monitoring dashboard for agencies"

**Pain points:**
- Need one dashboard that shows health across all client apps
- Can't afford per-seat pricing for clients who don't log in
- Need to be alerted before clients call them about broken jobs

**Why Crontinel:** Multi-app design (Team plan: unlimited apps). One account, one dashboard, all clients. $49/mo is trivial compared to one client complaint call.

---

## 8. Distribution Channels

Ranked by expected ROI relative to time investment. Focus the first 90 days on channels 1-5.

| Rank | Channel | Why | Time Investment |
|---|---|---|---|
| 1 | **r/laravel** | 90K members, tight community, high developer concentration | Medium (must not spam) |
| 2 | **Laravel News** | Newsletter reaches 30K+ Laravel devs weekly | Medium (submit + write) |
| 3 | **X / Twitter** | Laravel community active (#laravel tag, @taylorotwell, @laravelphp) | Low-Medium (daily) |
| 4 | **SEO / Blog** | Compound growth; pays off in 3-6 months | High (write consistently) |
| 5 | **GitHub** | OSS repo as marketing asset; README as landing page for devs | Low (maintain) |
| 6 | **Product Hunt** | Launch event; good for initial burst of signups | One-time (launch day) |
| 7 | **Hacker News** | "Show HN" post; lower Laravel concentration but high reach | One-time (launch day) |
| 8 | **DEV.to** | Good SEO value; Laravel devs present | Low (write occasionally) |
| 9 | **Laracasts Forum** | Smaller but highly engaged Laravel learning community | Low (be helpful) |
| 10 | **YouTube / Screencasts** | Highest conversion but highest effort | Defer to post-PMF |

### Channel-Specific Notes

**r/laravel:** Only post when you can add genuine value. Post format that works: "I built X, here's what I learned" (not "I built X, try it"). Share the open-source angle. Answer monitoring questions in other threads without plugging Crontinel unless directly relevant.

**X / Twitter:** Tweet about the problem, not the product. "Your cron jobs failed at 2am and you found out from a customer." Share behind-the-scenes building updates. Engage with @laravelphp, @Laracasts, @laravelnews accounts by replying with value, not ads.

**Laravel News:** Highest-quality Laravel audience. Submit the Composer package for review. If budget allows, consider a sponsored newsletter spot at launch ($199-500/issue). One issue reaches more qualified users than weeks of organic effort.

---

## 9. Launch Strategy

### Week 1: Soft Launch (Pre-announcement)

**Goal:** Get the house in order before driving traffic.

- [ ] Submit sitemap to GSC and Bing Webmaster Tools
- [ ] Create all comparison pages: /vs-cronitor, /vs-healthchecks
- [ ] Publish first two blog posts (install guide + Horizon monitoring guide)
- [ ] Set up OG images for all pages
- [ ] Verify Core Web Vitals (LCP < 2.5s, CLS < 0.1)
- [ ] Test sign-up flow end-to-end (free trial + Stripe Pro upgrade)
- [ ] Submit to Laravel News package directory
- [ ] Submit to AlternativeTo.net as alternative to Cronitor
- [ ] Submit to Made With Laravel, SaaSHub, StackShare

### Week 2: Product Hunt Launch

**Goal:** Public launch event for initial user burst.

- [ ] Schedule Product Hunt launch for Tuesday (highest traffic day)
- [ ] Write Hunter message: focus on problem, not features
- [ ] Prepare 5 screenshots + demo video (30-60 second walkthrough)
- [ ] Ask 10-15 developer friends to upvote and leave genuine comments
- [ ] Publish "Show HN" on the same day as PH launch
- [ ] Post in r/laravel: "I launched a free cron monitoring tool for Laravel" (not promotional — focus on the problem)
- [ ] Tweet the launch with a GIF/screenshot of the dashboard

### Week 3: Content and Community

**Goal:** Start building organic traction and community presence.

- [ ] Publish blog post #3 (the "Cronitor alternative" comparison)
- [ ] Answer 3-5 questions in r/laravel that mention monitoring, cron failures, or Horizon issues
- [ ] Post one thread on X about the problem: "3 symptoms your Laravel cron jobs are silently broken"
- [ ] Email early signups from PH launch: ask for feedback, offer to get on a 15-minute call
- [ ] Set up Plausible (or equivalent) analytics to track blog traffic

### Week 4: Double Down on What's Working

**Goal:** Identify top acquisition channel and invest more.

- [ ] Review GSC for any early keyword impressions (what are people finding Crontinel for?)
- [ ] Review Plausible for top traffic sources from launch week
- [ ] Publish blog post #4 (whichever topic shows search demand based on GSC data)
- [ ] If Product Hunt drove signups: engage those users directly, ask for testimonials
- [ ] If r/laravel drove signups: increase community presence
- [ ] Set up automated trial expiry email sequence if not done

---

## 10. Community Building

### r/laravel Strategy (How to Do It Without Being Spammy)

**The rule:** Give 5x before you take 1x. For every post about Crontinel, spend time answering 5 threads where you add value with no mention of Crontinel.

**What to post:**
- "I just launched an open-source cron monitoring tool for Laravel. Here's what I built and why." — shares the GitHub repo first, mentions the hosted service second
- Tutorials: "How I monitor Laravel Horizon in production" with an actual code walkthrough
- Case studies: "My cron job failed for 3 days and I didn't know — here's the system I built to prevent that"

**What never to post:**
- "Check out my tool, it does X" (pure promo)
- Replies in unrelated threads that mention Crontinel when it doesn't fit
- Anything that sounds like a marketing email

**How to build credibility over time:**
- Get your account to 100+ karma before posting about Crontinel
- Become known for helpful answers about Horizon and queue management
- When people ask "how do you monitor cron jobs?" — that's when you mention Crontinel naturally

**Cadence:** 2-3 relevant community posts per week. Never more than 1 Crontinel-specific post per week.

---

## 11. Paid Channels

### Should You Use Google Ads?

**Verdict: Not yet. Launch with $0 in paid ads. Revisit at $500 MRR.**

**Reasoning:**

At launch, you have no conversion data. Google Ads for "laravel cron monitoring" will cost $3-8/click (developer tool CPCs are high). Without knowing your conversion rate, you're spending blind.

First, collect organic data: which blog posts convert, which landing pages convert, what the free-to-paid upgrade rate looks like. Once you have a CAC target (e.g., "I can spend $50 to acquire a $19/mo customer"), run a small Google Ads test.

**When to start paid:**
- You have 20+ paying customers (proof the product converts)
- You know your trial-to-paid conversion rate
- You have $200-500/month to test with

**What to run when ready:**
- Search ads on "cronitor alternative," "laravel cron monitoring," "laravel horizon monitoring"
- Exact match + phrase match only (avoid broad match)
- Landing page: dedicated comparison page (/vs-cronitor), not the homepage
- Start with $10/day budget; scale only if CPA is acceptable

**What not to run:**
- Display ads (developer audience blocks ads)
- Social ads (Facebook/Instagram — wrong audience entirely)
- Broad keywords like "cron monitoring" (high CPC, low conversion)

---

## 12. KPIs to Track

### Monthly KPIs (review first Monday of each month)

| Metric | Source | Target at 90 days | Target at 6 months |
|---|---|---|---|
| Monthly signups | Auth logs / Plausible | 50 | 200 |
| MRR | Stripe | $200 | $1,000 |
| Free-to-paid conversion | Stripe / app data | 5% | 8% |
| Blog organic sessions | GSC / Plausible | 200/mo | 1,500/mo |
| Domain Rating (DR) | Ahrefs | 10 | 25 |
| Referring domains | Ahrefs | 20 | 60 |
| GitHub stars | GitHub | 100 | 400 |
| NPS / testimonials | Email | 3 testimonials | 10 testimonials |
| Churn rate | Stripe | < 10%/mo | < 6%/mo |

### Weekly KPIs (every Monday, 10 minutes)

- GSC clicks (vs. last week)
- New signups (vs. last week)
- Trial conversions (vs. last week)
- Any critical errors in ERRORS.md

### What to Do When Numbers Are Off

- MRR not growing: Check trial conversion — is the free-to-paid flow working? Is the trial expiry email going out?
- Blog traffic low after 60 days: Check GSC for indexing issues. Verify sitemap submission. Review content quality (are posts actually targeting a real keyword?).
- Signups low: Check PH + HN referral traffic. Is the sign-up form working? Is the free tier compelling enough?
- High churn: Talk to churned users. Usually means product doesn't deliver on the promise (cron jobs not being detected, alerts not firing, etc.).

---

## 13. 30-Day Sprint Plan

A concrete week-by-week checklist to execute during and after launch.

### Week 1 (Days 1-7): Foundation

- [ ] Verify sitemap covers all public pages; submit to GSC
- [ ] Verify robots.txt is correct and not blocking anything important
- [ ] Add Schema.org markup (SoftwareApplication, FAQPage on /pricing)
- [ ] Set up Plausible Analytics (or equivalent) on landing site
- [ ] Add OG image to all pages
- [ ] Submit Crontinel to AlternativeTo (alternative to Cronitor, Healthchecks.io)
- [ ] Submit to Made With Laravel, SaaSHub, StackShare
- [ ] Publish blog post #1: Laravel Horizon monitoring guide
- [ ] Publish blog post #2: Why Laravel cron jobs fail silently
- [ ] Write /vs-cronitor comparison page (publish before PH launch)

### Week 2 (Days 8-14): Launch Week

- [ ] Product Hunt launch (aim for Tuesday)
- [ ] Hacker News "Show HN" post (same day as PH)
- [ ] r/laravel launch post: "I built a free cron monitoring tool for Laravel"
- [ ] Tweet launch announcement
- [ ] Submit Crontinel to Laravel News package directory
- [ ] Email any beta users for upvotes and testimonials
- [ ] Set up basic email drip for trial users (day 1, day 7, day 14)

### Week 3 (Days 15-21): Content + Community

- [ ] Publish blog post #3: Cronitor vs. Crontinel comparison
- [ ] Answer 5 r/laravel questions about monitoring/Horizon/cron (no Crontinel mention unless naturally fits)
- [ ] Post one X thread about the pain of silent cron failures
- [ ] Review GSC: what queries are showing impressions? Write those posts next.
- [ ] Review sign-up funnel: where are people dropping off?
- [ ] Email all sign-ups from week 2: "What would make you upgrade?"

### Week 4 (Days 22-30): Double Down

- [ ] Publish blog post #4 (informed by GSC data from week 1-2)
- [ ] Write and submit guest post pitch to Laravel News
- [ ] Reach out to Freek Van der Hagen / Spatie about a Crontinel mention in their `schedule-monitor` docs
- [ ] Review first monthly KPIs snapshot
- [ ] Set next month's content calendar (4 more blog topics)
- [ ] If Product Hunt went well: ask top commenters for testimonials for landing page
- [ ] If no paid customers yet: review pricing page and free-to-paid CTA (is the upgrade trigger clear?)

---

## Appendix: Quick Reference

### Priority Actions This Week

1. Publish the Horizon monitoring blog post (most impactful for SEO + conversion)
2. Submit to Laravel News package directory
3. Add sitemap and Schema.org markup
4. Write /vs-cronitor comparison page

### Competitor Monitoring

Set Google Alerts for: "cronitor," "healthchecks.io," "laravel monitoring," "laravel cron." Review monthly. Track when competitors add features or raise prices — update comparison pages within 48 hours.

### Content Writing Rule

Every blog post uses Opus (claude-opus-4-6). No AI patterns. Read it out loud before publishing. If it sounds like a press release, rewrite it.
