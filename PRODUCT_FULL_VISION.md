
# Crontinel: Full Product Vision

## 1. What Crontinel IS

Crontinel is the monitoring tool that sees inside your Laravel application, not just outside it. While traditional uptime monitors ping your URLs and hope for the best, Crontinel ships as a Composer package that hooks directly into Horizon's Redis keys, reads queue connection configs, and subscribes to scheduler events. It knows which supervisor is paused, which queue is backing up, and which scheduled task silently failed at 3am. The open-source package handles local monitoring and alerting; the SaaS layer adds multi-app dashboards, hosted alerting, status pages, and historical analytics. Think of it as the Sentry model applied to infrastructure monitoring: free OSS package, paid cloud for teams that need more.

---

## 2. Competitive Landscape

### UptimeRobot

**What they do:** HTTP, HTTPS, ping, port, SSL, DNS, and keyword monitoring from 30+ global locations. Status pages, maintenance windows, mobile apps.

**Strengths:**
- Generous free tier (50 monitors at 5-minute intervals)
- Simple setup, no code changes required
- Large global check network
- Well-known brand, trusted by millions of sites
- Mobile app with push notifications

**Weaknesses:**
- Purely external. Cannot see inside your application.
- No cron or queue monitoring
- No framework-level integration
- Free tier limited to 5-minute intervals (a lot can go wrong in 5 minutes)
- Status pages are basic on free/lower tiers
- No incident management or on-call scheduling

**Pricing:** Free (50 monitors, 5-min), Pro $7/mo (50 monitors, 1-min), Business $21/mo (100 monitors), Enterprise $37/mo (200 monitors).

---

### Cronitor

**What they do:** Cron job monitoring, heartbeat checks, telemetry collection. Dashboard with job run history, environment awareness, CI/CD integration.

**Strengths:**
- Purpose-built for cron and job monitoring
- Telemetry features (duration, exit code, output capture)
- Environment-aware (staging vs production)
- Good CI/CD integration
- Clean dashboard

**Weaknesses:**
- No deep framework integration. Requires manual instrumentation or wrapper scripts.
- No queue depth or Horizon monitoring
- No external uptime monitoring
- Pricing scales with monitor count
- No MCP or AI integration

**Pricing:** Free (5 monitors), Developer $20/mo (unlimited monitors), Team $40/mo, Business $100/mo.

---

### Better Stack (formerly Better Uptime)

**What they do:** Uptime monitoring, incident management, on-call scheduling, status pages, and log management. Modern, well-designed UI.

**Strengths:**
- All-in-one platform (monitoring + incidents + on-call + logs)
- Beautiful UI, modern design
- Incident management with escalation policies
- Status pages included
- Log management integration

**Weaknesses:**
- No application-level monitoring (queues, Horizon, scheduled tasks)
- Heartbeat monitoring is basic (ping-based, no telemetry)
- Pricing gets expensive quickly for teams
- Log management competes with dedicated tools but lacks their depth
- No framework-specific integrations

**Pricing:** Free (10 monitors), Freelancer $20/mo, Small Team $36/mo, Business $80/mo.

---

### Healthchecks.io

**What they do:** Dead-man-switch heartbeat monitoring. Your cron pings a URL; if it stops pinging, you get alerted. Open source, self-hostable.

**Strengths:**
- Extremely simple concept, easy to set up
- Generous free tier (20 checks)
- Open source (can self-host)
- Supports cron expression validation
- Lightweight, does one thing well

**Weaknesses:**
- Only heartbeat monitoring. No queue depth, no Horizon, no uptime checks.
- Binary: "it ran" or "it didn't." No telemetry on what happened.
- No dashboard for job output or failure analysis
- No status pages
- No incident management
- Minimal alerting options on free tier

**Pricing:** Free (20 checks), Hobbyist $20/mo (100 checks), Business $80/mo (1000 checks), Enterprise custom.

---

### Oh Dear

**What they do:** Uptime, SSL, broken links, mixed content, DNS, and performance monitoring. Built by Spatie, deeply connected to the Laravel ecosystem.

**Strengths:**
- Laravel ecosystem credibility (Spatie team)
- Unique checks: broken links, mixed content, DNS
- Application health check integration (via Spatie health package)
- Clean, developer-friendly UI
- Good documentation

**Weaknesses:**
- No cron job or queue monitoring
- No Horizon integration
- No heartbeat/dead-man-switch monitoring
- Relatively expensive for what you get
- Small team, slower feature development
- No AI/MCP integration

**Pricing:** Solo $19/mo (5 sites), Team $49/mo (20 sites), Business $99/mo (100 sites).

---

### Datadog

**What they do:** Enterprise-grade observability platform. APM, logs, metrics, traces, synthetics, security monitoring, network monitoring, and more.

**Strengths:**
- Comprehensive: if it exists, Datadog probably monitors it
- Powerful dashboards and alerting
- APM with distributed tracing
- Synthetic monitoring (browser and API)
- Massive ecosystem of integrations
- Enterprise support and compliance certifications

**Weaknesses:**
- Extremely expensive. Costs spiral unpredictably with data volume.
- Complex setup, steep learning curve
- Overkill for most Laravel applications
- Agent-based (requires infrastructure access)
- No Laravel-specific intelligence (Horizon, queue configs, scheduler)
- Pricing model penalizes growth

**Pricing:** Free (limited), Pro $15/host/mo, Enterprise $23/host/mo. But real costs include per-GB log ingestion, per-host APM, per-10k synthetic tests. A typical mid-size app can easily hit $500+/mo.

---

### Grafana + Prometheus

**What they do:** Self-hosted observability stack. Prometheus scrapes metrics; Grafana visualizes them. Extensible with Loki (logs) and Tempo (traces).

**Strengths:**
- Free and open source
- Extremely powerful and flexible
- Industry standard for metrics and visualization
- Huge community and ecosystem
- Full control over data

**Weaknesses:**
- Requires significant DevOps expertise to set up and maintain
- Self-hosted means you manage infrastructure, backups, scaling
- No built-in alerting UX (Alertmanager exists but is clunky)
- No framework-level auto-discovery
- High operational overhead
- No status pages, no incident management

**Pricing:** Free (self-hosted). Grafana Cloud starts at $0 (limited), Pro $8/user/mo.

---

### Laravel Forge Heartbeats

**What they do:** Basic ping-based heartbeat monitoring for scheduled tasks. Included with Forge subscription.

**Strengths:**
- Already included if you use Forge
- Zero additional cost
- Simple to configure within Forge UI
- Tight Forge integration

**Weaknesses:**
- Only heartbeat monitoring (did it run or not)
- No telemetry (duration, exit code, output)
- No queue monitoring, no Horizon monitoring
- No external uptime monitoring
- No alerting customization (just email)
- No dashboard, no history
- Requires Forge subscription

**Pricing:** Included with Forge ($12-39/mo).

---

### Hyperping

**What they do:** HTTP uptime monitoring with status pages. Simple, focused, competitive pricing.

**Strengths:**
- Clean UI, easy setup
- Competitive pricing for uptime monitoring
- Status pages included
- Multiple check locations
- Good API

**Weaknesses:**
- HTTP-only, no cron or queue monitoring
- No framework integration
- Smaller company, less feature breadth
- No incident management
- No on-call scheduling

**Pricing:** Free (10 monitors), Starter $9.90/mo (50 monitors), Growth $29/mo (200 monitors), Business $79/mo (1000 monitors).

---

### Comparison Table

| Feature | Crontinel | UptimeRobot | Cronitor | Better Stack | Healthchecks | Oh Dear | Datadog | Grafana/Prom | Forge | Hyperping |
|---|---|---|---|---|---|---|---|---|---|---|
| Cron monitoring | Deep | No | Yes | Basic | Heartbeat | No | Manual | Manual | Heartbeat | No |
| Queue monitoring | Deep | No | No | No | No | No | Manual | Manual | No | No |
| Horizon monitoring | Yes | No | No | No | No | No | No | No | No | No |
| HTTP uptime | Phase 2 | Yes | No | Yes | No | Yes | Yes | Yes | No | Yes |
| Status pages | Phase 3 | Yes | No | Yes | No | No | No | No | No | Yes |
| Incident mgmt | Phase 3 | No | No | Yes | No | No | Yes | No | No | No |
| On-call | Phase 3 | No | No | Yes | No | No | Yes | No | No | No |
| MCP/AI | Yes | No | No | No | No | No | No | No | No | No |
| Laravel-native | Yes | No | No | No | No | Partial | No | No | Partial | No |
| OSS package | Yes | No | No | No | Yes | No | No | Yes | No | No |
| Free tier monitors | 5 | 50 | 5 | 10 | 20 | 0 | Limited | Unlimited | N/A | 10 |
| Starting paid price | $19/mo | $7/mo | $20/mo | $20/mo | $20/mo | $19/mo | $15/host | Free | $12/mo | $9.90/mo |

---

## 3. Crontinel's Unfair Advantages

### Laravel-Native Composer Package with Auto-Discovery

Install with `composer require crontinel/laravel`. That is it. Laravel's package auto-discovery registers the service provider, publishes the config, and Crontinel starts monitoring. No agents to install, no infrastructure to manage, no wrappers to add around your cron commands. Every other monitoring tool requires you to come to them. Crontinel comes to you.

### Deep Framework Integration

Crontinel does not treat your application as a black box. It reads Horizon's Redis keys to know supervisor status in real time. It queries queue database tables and Redis lists to measure depth, age, and failure rates per queue. It hooks into the scheduler's event system to capture exit codes, durations, and output. This level of integration is possible because Crontinel is a PHP package running inside your application process, not an external agent polling endpoints.

### MCP Server for AI Assistants

No other monitoring tool offers an MCP server. Developers using Claude Code, Cursor, or other AI assistants can query their monitoring data conversationally: "Which queues are backing up?" or "Show me failed jobs in the last hour." This is a new category. Being first in AI-native monitoring creates mindshare that is difficult to displace.

### OSS + SaaS Model (The Sentry Playbook)

The MIT-licensed Composer package is free forever. Developers adopt it because it solves a real problem with zero financial commitment. The SaaS layer captures revenue from teams that need hosted alerting, multi-app dashboards, history retention, and status pages. This model has been proven by Sentry, GitLab, and PostHog. Adoption drives awareness; awareness drives SaaS conversions.

### Unlimited Monitors on Paid Plans

Cronitor, UptimeRobot, and Hyperping all gate monitor count behind pricing tiers. Crontinel's Pro plan includes unlimited monitors for $19/mo. For a developer with 50 scheduled tasks, 10 queues, and 3 Horizon supervisors, that is 63 monitors. On Cronitor, that requires the Team plan at $40/mo minimum. On UptimeRobot, that is the Business tier. Unlimited monitors removes friction entirely.

### Zero-Config for Laravel Apps

Crontinel auto-discovers scheduled tasks from the Kernel, detects queue connections from `config/queue.php`, and finds Horizon supervisors from `config/horizon.php`. The default configuration monitors everything out of the box. Other tools require you to register each monitor manually.

### Per-Job Failure Analysis

Healthchecks.io tells you "your job didn't ping." Cronitor tells you "your job ran and took 45 seconds." Crontinel tells you "your job ran, took 45 seconds, exited with code 1, threw an `Illuminate\Database\QueryException` on line 87 of `ProcessPayments.php`, and the queue it depends on has 4,200 pending jobs." Context matters when you are debugging at 3am.

---

## 4. Product Roadmap

### Phase 1: Launch (Weeks 0-4) — Current State

**Scope:** Ship the core package and SaaS MVP.

| Feature | Status | Effort |
|---|---|---|
| Horizon supervisor monitoring | Built | — |
| Queue depth, failed jobs, oldest job age | Built | — |
| Cron/scheduled task monitoring (exit code, duration, late detection) | Built | — |
| Alert channels: Slack, email, PagerDuty, webhooks | Built | — |
| REST API | Built | — |
| MCP server for AI assistants | Built | — |
| Local Blade dashboard | Built | — |
| SaaS dashboard | Built | — |
| CLI health checks (`php artisan crontinel:check`) | Built | — |
| Documentation site | In progress | ~1 week |
| Packagist release and onboarding flow | In progress | ~1 week |

**Phase 1 total remaining effort:** ~2 weeks of focused work.

**Key risk:** Documentation quality determines first impressions. Laravel developers expect excellent docs (see Spatie's packages as the benchmark).

---

### Phase 2: External Monitoring (Months 2-4)

**Scope:** Add the table-stakes features that competitors already have. This makes Crontinel a complete replacement, not just a supplement.

| Feature | Effort Estimate | Notes |
|---|---|---|
| HTTP/HTTPS endpoint monitoring | ~2 weeks | Build check runner, result storage, multi-location dispatch |
| Ping and port monitoring | ~3 days | Extend check runner with ICMP and TCP socket checks |
| SSL certificate expiry alerts | ~2 days | Piggyback on HTTPS checks, parse cert chain |
| DNS record change monitoring | ~3 days | Periodic DNS lookups, diff against stored records |
| Response time tracking (P50/P95/P99) | ~1 week | Aggregate stored check results, build graph endpoints |
| Keyword presence/absence detection | ~2 days | Regex/string match on HTTP response body |
| Configurable check intervals (30s to 24hr) | ~3 days | Scheduler with per-monitor interval config |
| Multi-region check locations (3 regions initially) | ~2 weeks | Deploy check runners to 3 cloud regions, coordinate results |

**Phase 2 total effort:** ~6-7 weeks of engineering.

**Key trade-offs:**
- Multi-region requires infrastructure spend. Each region needs a check runner process. Starting with 3 regions (US-East, EU-West, AP-Southeast) keeps costs manageable at ~$30-50/mo per region for small VPS instances.
- Check intervals below 60 seconds create significant data volume. Need to design retention policies early.
- HTTP monitoring is a crowded space. Crontinel's differentiator here is that it bundles internal + external monitoring. A developer should not need two tools.

---

### Phase 3: Incident Management and Status Pages (Months 4-7)

**Scope:** Transform Crontinel from a monitoring tool into an incident response platform.

| Feature | Effort Estimate | Notes |
|---|---|---|
| Public branded status pages (path-based) | ~2 weeks | Subdomain and custom domain support follow later |
| Manual incident management (create, update, resolve) | ~1 week | CRUD with timeline, affected monitors |
| Automatic incident creation from monitor state changes | ~1 week | State machine: healthy > degraded > down > recovering |
| On-call scheduling and escalation policies | ~3 weeks | Complex: rotation schedules, escalation chains, overrides |
| SMS alerting via Twilio | ~3 days | Twilio API integration, phone number verification |
| Push notifications (Telegram, Discord, Pushover) | ~1 week | Three integrations, each ~2 days |
| Status page subscriber notifications | ~1 week | Email/SMS opt-in, notification dispatch on status change |
| Status page API and embeddable badges | ~3 days | JSON API + SVG badge generator |
| Maintenance windows | ~3 days | Scheduled suppression rules, UI for scheduling |
| Subdomain and custom domain status pages | ~1 week | DNS verification, SSL provisioning via Let's Encrypt |

**Phase 3 total effort:** ~10-11 weeks of engineering.

**Key trade-offs:**
- On-call scheduling is the hardest feature in this phase. Rotation logic, timezone handling, override rules, and escalation chains are deceptively complex. Consider shipping a simplified version first (primary + backup, linear escalation) and iterating.
- Custom domain status pages require SSL certificate provisioning. Caddy or a managed load balancer with automatic HTTPS simplifies this significantly.
- SMS alerting introduces per-message cost. Must be gated to paid plans and rate-limited to prevent abuse.

---

### Phase 4: Intelligence and Scale (Months 7-12)

**Scope:** Add the features that justify Team and Enterprise pricing. Move from reactive alerting to proactive intelligence.

| Feature | Effort Estimate | Notes |
|---|---|---|
| Anomaly detection (learn normal patterns) | ~4 weeks | Statistical baseline (no ML needed initially; Z-score on historical data) |
| AI-powered root cause suggestions | ~3 weeks | Correlate events across monitors, LLM-generated summaries |
| Historical SLA reports (PDF/CSV export) | ~1 week | Uptime calculation, PDF generation |
| Response time trend analysis with degradation alerts | ~1 week | Rolling averages, threshold crossing detection |
| Team RBAC (owner, admin, member, viewer) | ~2 weeks | Permission system, invitation flow, UI |
| Audit logs | ~1 week | Event sourcing for all config changes |
| SSO/SAML | ~2 weeks | SAML 2.0 integration, enterprise auth flow |
| Public webhook system | ~1 week | Outgoing webhooks with retry, signature verification |
| Mobile app (iOS/Android) | ~8-10 weeks | React Native or Flutter; push notification integration |

**Phase 4 total effort:** ~24-26 weeks of engineering.

**Key trade-offs:**
- "ML-based anomaly detection" sounds impressive but start simple. A Z-score anomaly detector on 7-day rolling windows catches 80% of meaningful deviations. Upgrade to something more sophisticated only when customers demand it.
- The mobile app is the largest single investment. Delay it until monthly revenue justifies the maintenance burden. Push notifications via Telegram and email cover most urgent alerting needs.
- SSO/SAML is a checkbox feature for enterprise sales. It is tedious to build but necessary for the Enterprise tier.
- AI root cause suggestions are a natural extension of the MCP server. Use the same LLM infrastructure; just run correlation queries automatically instead of waiting for a human to ask.

---

### Phase 5: Platform (Months 12-18)

**Scope:** Expand beyond Laravel. Become the monitoring platform for application developers, not just Laravel developers.

| Feature | Effort Estimate | Notes |
|---|---|---|
| Multi-framework support (Sidekiq, Celery, BullMQ) | ~4 weeks per framework | Each requires deep integration work similar to the Laravel package |
| Synthetic monitoring (Playwright-based browser checks) | ~4 weeks | Headless browser infrastructure, script editor UI |
| API monitoring (multi-step sequence tests) | ~3 weeks | Step builder, variable extraction, assertion engine |
| Log ingestion and search | ~6 weeks | Ingestion pipeline, storage (ClickHouse or similar), search UI |
| Custom metric ingestion | ~2 weeks | Push API, threshold configuration, graph rendering |
| White-label status pages for agencies | ~3 weeks | Branding removal, custom CSS, agency billing model |
| Enterprise tier (dedicated support, SLA, data residency) | ~2 weeks | Mostly operational: contracts, SLA definitions, isolated infra |

**Phase 5 total effort:** ~28-32 weeks of engineering (assuming 3 framework integrations).

**Key trade-offs:**
- Multi-framework support is the biggest bet. Each framework integration requires the same depth of knowledge that makes the Laravel package special. Hiring or contracting Ruby/Python/Node specialists is likely necessary.
- Log ingestion competes with Datadog, Logtail, and Papertrail. Keep it intentionally limited: recent logs, basic search, correlation with monitors. Do not try to build a full log analytics platform.
- Synthetic monitoring requires headless browser infrastructure. This is expensive to run and maintain. Consider partnering with a headless browser provider or running on-demand containers.
- White-label status pages target a specific audience (agencies managing client infrastructure). Validate demand before building.

---

## 5. Pricing Model Evolution

### Launch (Phase 1)

| | Free | Pro | Team |
|---|---|---|---|
| Price | $0/mo | $19/mo | $49/mo |
| Apps | 1 | 5 | Unlimited |
| Internal monitors | 5 | Unlimited | Unlimited |
| History | 7 days | 90 days | 1 year |
| Alerts | None | All channels | All channels + custom rules |
| API access | No | Yes | Yes |
| Status pages | No | 1 per app | Unlimited |
| MCP server | Yes | Yes | Yes |

### After Phase 2 (External Monitoring Added)

| | Free | Pro | Team |
|---|---|---|---|
| Price | $0/mo | $19/mo | $49/mo |
| External monitors | 3 (5-min interval) | Unlimited (1-min) | Unlimited (30s) |
| Check regions | 1 | 3 | All available |
| SSL/DNS monitoring | No | Yes | Yes |

External monitoring is bundled into existing tiers. The value proposition of Pro becomes overwhelming: unlimited internal monitors, unlimited external monitors, all alert channels, API access, and a status page for $19/mo. This is the growth lever.

### After Phase 3 (Incidents and Status Pages)

| | Free | Pro | Team |
|---|---|---|---|
| Status pages | No | 1 per app (path-based) | Unlimited (custom domain) |
| Incident management | No | Manual only | Auto + manual |
| On-call scheduling | No | No | Yes |
| SMS alerts | No | No | Included (fair use) |
| Maintenance windows | No | Yes | Yes |

On-call and SMS are Team-tier differentiators. These features have real marginal cost (Twilio) and operational complexity that justifies the higher price.

### After Phase 4 (Enterprise Tier Introduced)

| | Free | Pro | Team | Enterprise |
|---|---|---|---|---|
| Price | $0/mo | $19/mo | $49/mo | $199/mo (starting) |
| Anomaly detection | No | No | Yes | Yes |
| AI root cause | No | No | Basic | Advanced |
| SLA reports | No | No | Yes | Yes + custom |
| RBAC | No | No | Yes (4 roles) | Yes + custom roles |
| SSO/SAML | No | No | No | Yes |
| Audit logs | No | No | 30 days | 1 year |
| Mobile app | No | Yes | Yes | Yes |
| Support | Community | Email | Priority email | Dedicated Slack + SLA |

### After Phase 5 (Full Platform)

| | Free | Pro | Team | Enterprise |
|---|---|---|---|---|
| Price | $0/mo | $19/mo | $49/mo | Custom ($199+) |
| Multi-framework | Laravel only | Laravel only | Any supported | Any + custom |
| Synthetic monitoring | No | No | 5 checks | Unlimited |
| API monitoring | No | No | 10 sequences | Unlimited |
| Log ingestion | No | No | 1 GB/mo | Custom |
| Custom metrics | No | 5 metrics | 50 metrics | Unlimited |
| White-label | No | No | No | Available (add-on) |
| Data residency | Default | Default | Default | Choice of region |

**Pricing philosophy:** Never raise prices on existing tiers. Instead, add features to higher tiers and introduce the Enterprise tier as the ceiling. The $19 Pro plan stays at $19 forever. It is the anchor that drives adoption. Revenue growth comes from Team and Enterprise conversions, not from squeezing Pro users.

---

## 6. The Permanent Moat

Features are not a moat. Every feature listed in this document can be copied by a funded competitor in 12-18 months. Crontinel's moat is structural, built on three layers that compound over time.

### Layer 1: Deep Framework Integration

Crontinel's Composer package reads Horizon's Redis keys (`horizon:supervisor:*`, `horizon:masters`), parses queue connection configurations from `config/queue.php`, and hooks into Laravel's `Schedule` class via event listeners. It understands the difference between a `database` queue connection and a `redis` queue connection because it reads the same config files your application reads. It knows when a supervisor is paused because it watches the same Redis keys Horizon watches.

This level of integration requires deep, ongoing knowledge of Laravel internals. When Laravel 12 ships, Crontinel's package must be updated to handle any changes to Horizon's Redis key structure, queue table schemas, or scheduler event signatures. This is a maintenance burden, but it is also a barrier. A competitor building "Laravel monitoring" from the outside cannot achieve this depth without investing the same effort.

### Layer 2: AI-Native Monitoring (MCP Server)

The MCP server is not a gimmick. It represents a fundamental shift in how developers interact with monitoring data. Instead of opening a dashboard, scanning graphs, and forming hypotheses, a developer asks their AI assistant: "Why is the payment queue slow?" The MCP server provides the context; the AI provides the analysis.

Being first in this category matters. Developers who adopt Crontinel's MCP server build workflows around it. Their AI assistants learn to query Crontinel's data. Switching to a competitor means retraining habits, rebuilding prompts, and losing conversational context. This is soft lock-in, but it is real.

As AI assistants become the primary interface for development work (and the trend is unmistakable), the monitoring tool that integrates best with those assistants captures a permanent advantage.

### Layer 3: Open Source Community

The MIT-licensed Composer package creates a flywheel. Developers install it for free. Some contribute bug fixes, features, and documentation. The package improves. More developers install it. The community grows. Community members become SaaS customers. SaaS revenue funds further development.

This flywheel is difficult to disrupt because it is distributed. The package lives in thousands of `composer.json` files. Removing it requires effort; keeping it requires none. Inertia favors the installed package.

Competitors can build their own open-source packages, but they start at zero adoption. Crontinel's head start compounds with every `composer require`.

### The Compound Effect

Each moat layer reinforces the others. Deep integration makes the OSS package valuable, which drives adoption, which grows the community, which improves the package, which makes the MCP server more useful, which attracts AI-native developers, who contribute back to the OSS package.

A competitor would need to simultaneously: (1) build deep Laravel integration, (2) ship an MCP server, and (3) grow an open-source community. Doing all three at once, while Crontinel already has a head start, is the kind of challenge that makes investors look elsewhere.

That is the moat. Not a feature list. A compounding system.

---

*Last updated: April 2026*
