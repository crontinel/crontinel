# Crontinel Launch Positioning Pack

Last updated: 2026-04-08

---

## 1. Product Positioning Statement

Crontinel is a Laravel-native monitoring tool that tells you when your scheduled tasks stop running, your queues stop draining, or your Horizon workers go silent. One Composer package, no infrastructure to manage, alerts in minutes instead of finding out from a customer complaint days later.

---

## 2. Comparison Angles vs Generic Monitoring Tools

| Competitor | Their focus | Where Crontinel wins | Their advantage | When to recommend them instead |
|---|---|---|---|---|
| **Healthchecks.io** | Generic heartbeat/ping monitoring, language-agnostic | Crontinel reads Laravel internals (queue depth, Horizon worker state, scheduler output) instead of waiting for a dumb ping. No curl calls at the end of scripts. Unlimited monitors at $19/mo vs per-check pricing. | Free tier with 20 checks, open-source, battle-tested since 2015. Broader language support. | If the team runs non-Laravel apps and only needs "did this cron run yes/no" checks across multiple stacks. |
| **Cronitor** | General-purpose cron and job monitoring | Laravel Composer package with auto-discovery vs. manual HTTP ping setup. Unlimited monitors on every paid plan vs. Cronitor's per-monitor tiers (20 monitors at $20/mo). Horizon-aware, not just heartbeat-aware. | Mature product, wide language support, established brand trust. Better CI/CD job monitoring. | If the team needs cross-platform cron monitoring (Python, Node, Go) and Laravel is only one piece. |
| **Better Stack** | Full observability suite (uptime, logs, on-call, status pages) | Crontinel costs $19/mo vs. Better Stack's $50+/mo for comparable cron coverage. Purpose-built for the job vs. cron monitoring bolted onto a platform play. Zero config overhead. | All-in-one platform: logs, uptime, incident management, on-call rotation in one bill. | If the team wants to consolidate uptime + logging + on-call + cron into a single vendor and has the budget. |
| **Oh Dear** | Uptime, SSL, broken links, performance monitoring (Laravel ecosystem) | Crontinel covers queue health and Horizon worker state, which Oh Dear doesn't touch. Deeper scheduler diagnostics (not just "did it run" but "did it succeed, what was the output"). | Built by Spatie, strong Laravel community trust. Excellent uptime/SSL/mixed-check monitoring. | If the primary need is uptime/SSL monitoring and scheduled task checks are secondary. Complementary tools, not competitors. |
| **Hyperping** | HTTP uptime monitoring and status pages | Crontinel monitors background processes that HTTP checks can't see. A health endpoint returning 200 says nothing about whether your nightly billing sync ran. Fundamentally different coverage. | Clean UI, good status page product, competitive pricing on uptime checks. | If the need is pure HTTP uptime monitoring. Hyperping and Crontinel solve different problems. |

---

## 3. Who Crontinel Is For / Not For

### Ideal customers

| Segment | Description | Why they buy |
|---|---|---|
| **Solo Laravel dev with 1-3 production apps** | Runs scheduled tasks for backups, report generation, API syncs. No ops team. Checks Horizon manually or not at all. | Can't afford silent failures. No time to build custom monitoring. $19/mo is cheaper than one lost customer from a missed billing sync. |
| **Small Laravel agency (2-5 devs)** | Manages multiple client apps on Forge/Vapor. Each app has its own scheduler and queue setup. | Needs multi-app visibility from one dashboard. Client SLAs depend on background jobs running. The Team plan ($49/mo) covers all client apps. |
| **Startup with Laravel monolith, pre-Series A** | Product relies on background processing: webhook handlers, data pipelines, scheduled reports for customers. 1-2 engineers handling ops alongside feature work. | Background job failures directly cause customer churn. No dedicated DevOps to build monitoring. Composer require + API key is their speed. |
| **Laravel dev who already got burned** | Had a cron fail silently, lost data, got an angry customer email, spent a weekend debugging. Knows the pain, actively looking for a fix. | Emotional buyer. The "never again" motivation. Will pay immediately, least price-sensitive segment. |
| **Teams using Horizon in production** | Run Redis queues with Horizon for job processing. Need to know when workers die, queues back up, or jobs stall. | Horizon's dashboard shows current state but doesn't alert on degradation. Crontinel fills that gap specifically. |

### Not ideal customers

| Segment | Why not |
|---|---|
| **Non-Laravel PHP apps** | The Composer package is Laravel-specific. Generic PHP cron jobs are better served by Healthchecks.io or Cronitor. |
| **Teams that need full observability (logs + traces + metrics)** | Crontinel monitors background job health, not application performance. Point them to Better Stack, Datadog, or New Relic. |
| **Enterprise with existing Prometheus/Grafana stack** | They already have the infrastructure to monitor everything. Crontinel adds value only if their existing stack has a blind spot on scheduler/queue health, which is possible but not guaranteed. |
| **Hobbyists with no production traffic** | If nobody depends on the cron jobs running, monitoring them is overkill. The free tier exists for this segment, but they won't convert to paid. |
| **Teams that only need uptime monitoring** | Wrong tool. Recommend Oh Dear, Hyperping, or Better Stack instead. |

---

## 4. Message Angles for Landing, Docs, and Outreach

1. **Your health check returns 200. Your nightly data sync hasn't run in six days. Crontinel covers the gap between "site is up" and "everything is actually working."**

2. **One `composer require`, one API key, done. Crontinel auto-discovers your scheduled tasks and queue connections. No agents, no config files, no new servers.**

3. **Horizon says "active." But are jobs actually processing? Crontinel tracks queue depth, worker throughput, and oldest pending job age so you know the difference between running and working.**

4. **Every Laravel app with scheduled tasks has had the "why didn't the backup run" panic. Crontinel is five minutes of setup vs. the 3 AM incident response.**

5. **Unlimited monitors on every paid plan. Cronitor charges per monitor, which punishes you for being thorough. Add as many monitors as you need without watching the bill.**

6. **The hardest production failure to catch is a process that quietly stops. No error, no log, no alert. Crontinel is a dead man's switch for your background work.**

7. **Free and open source for local use. Connect to the cloud when you want alerts, history, and multi-app monitoring. The Sentry model, applied to cron and queue health.**

8. **Forge heartbeats tell you schedule:run was called. They don't tell you if a specific task inside the scheduler failed, if queue depth is climbing, or if Horizon workers are stuck. Crontinel goes one layer deeper.**

9. **Your billing sync, your nightly report, your webhook processor: these aren't infrastructure. They're product features your customers depend on. Monitor them like it.**

10. **Built for Laravel, not adapted from generic tooling. Crontinel understands artisan commands, Horizon supervisors, and queue connections natively, because it runs inside your app, not outside it.**

---

## 5. Top 5 Objections and Responses

### "I'll just use Healthchecks.io, it's free"

Healthchecks.io is solid for generic heartbeat monitoring, and the free tier is generous. The difference: Healthchecks only knows whether a ping arrived. It doesn't know what happened inside your Laravel app. Queue depth growing, Horizon workers stuck in a reconnect loop, a scheduled task that ran but threw a silent exception: none of that generates a ping, so none of it triggers an alert. If your monitoring needs stop at "did the cron run yes/no," Healthchecks works. If you need to know whether your background processing is actually healthy, that's where Crontinel picks up.

### "I can monitor this myself with a custom health endpoint"

You absolutely can, and many teams do. The question is whether you want to maintain that code over time: handling alert deduplication, building a dashboard, tracking history, covering edge cases like Horizon paused vs. crashed, queue connection drops, scheduler process killed after a deploy. Crontinel packages all of that so you're not rebuilding monitoring infrastructure every time you add an app. If you've already built it and it works, keep it. If you haven't started, the Composer package saves you a few weekends.

### "Too many monitoring tools already"

Fair. Nobody wants another dashboard to check. Crontinel specifically covers the blind spot that existing tools miss: background job health. Your APM tracks request performance. Your uptime monitor checks HTTP endpoints. Your error tracker catches exceptions. None of them tell you that your nightly billing sync quietly stopped three days ago. If your current stack already covers scheduler and queue internals, you don't need this. Most stacks don't.

### "It's new, how do I know it won't disappear in six months?"

Legitimate concern with any new tool. Two things that reduce the risk: the core package is open source and MIT-licensed, so even if the SaaS disappeared tomorrow, you'd still have the local monitoring. And the SaaS funds continued development, so there's a business model behind it, not just a side project. Check the commit history and the changelog. But also, if you need a tool with five years of track record, Cronitor and Healthchecks.io exist. Crontinel is for people who value Laravel-native integration more than brand tenure.

### "What about uptime monitoring? I need that too."

Crontinel doesn't do HTTP uptime monitoring, and it's not trying to. Use Oh Dear, Hyperping, Better Stack, or whatever you already have for that. Crontinel covers the other half: did your scheduled tasks run, are your queues draining, are your workers healthy. They're complementary tools. Most teams end up with an uptime monitor plus a background job monitor because they solve fundamentally different problems. A 200 response from your homepage tells you nothing about whether your invoice generation cron ran last night.
