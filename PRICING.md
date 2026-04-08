# Crontinel Pricing Decision Pack

Last updated: 2026-04-08

---

## 1. Recommended Model: Flat Subscription Tiers (per-team)

**The model already on the landing page is correct. Keep it.**

Flat tiers gated by app count, monitor limits, and feature access. Billing attached to the Team entity. No per-seat charges, no metered usage billing.

Why this model wins for Crontinel at launch:

- **Predictable revenue.** Metered/usage-based pricing is hard to forecast and harder to implement correctly in Cashier. Flat tiers are one Stripe Price ID each.
- **Low friction adoption.** Developers hate usage surprises. "5 apps, unlimited monitors" is immediately understood. Per-monitor pricing (Cronitor's model) creates anxiety about adding monitors.
- **Matches the competitive sweet spot.** Oh Dear and Healthchecks.io both use flat tiers. Cronitor and Better Stack use per-monitor/add-on pricing and get complaints about cost unpredictability.
- **Solo founder simplicity.** One Cashier subscription per team, three plan slugs (free/pro/team), done. No metering infrastructure, no invoice line-item complexity.

Models explicitly rejected:

| Model | Why not |
|---|---|
| Per-monitor | Penalizes thorough monitoring; users add fewer monitors to save money, which defeats the product's purpose |
| Per-seat | Memory note says "don't suggest per-seat pricing." Also wrong fit: monitoring tools are infrastructure, not collaboration tools |
| Usage-based (events/pings) | Requires metering pipeline, creates billing surprises, terrible for a pre-revenue solo product |

---

## 2. Three Pricing Options

### Option A: Current pricing (RECOMMENDED)

| | Free | Pro | Team |
|---|---|---|---|
| Price | $0 | $19/mo ($182/yr) | $49/mo ($470/yr) |
| Apps | 1 | 5 | Unlimited |
| Monitors/app | 5 | Unlimited | Unlimited |
| History | 7 days | 90 days | 1 year |
| Team members | 1 | 3 | Unlimited |
| Alerts | No | Yes (Slack, email, PagerDuty, webhook) | Yes (all channels) |
| Status pages | No | 1 per app | Unlimited |
| REST API | No | Yes | Yes |
| Custom alert rules | No | No | Yes |
| Support | Community | Community | Priority (24h email) |

**Pros:**
- Already built into the landing page, PlanLimits service, and FAQ copy
- $19 Pro sits below Cronitor ($20 Developer) and Hyperping ($29 Basic) while offering more monitors
- $49 Team undercuts Better Stack's comparable setup ($21/50 monitors + $29/responder = $50+) and Cronitor Business ($50 for only 50 monitors)
- Clean 2.5x jump from Pro to Team signals clear value step-up
- 20% annual discount is standard and already coded into the toggle

**Cons:**
- $19 might leave money on the table once product-market fit is proven
- No middle ground between 5 apps (Pro) and unlimited (Team), which could cause a cliff

**Verdict: Ship this. It is the right price for a new entrant with zero brand recognition.**

### Option B: Lower Pro, higher Team

| | Free | Pro | Team |
|---|---|---|---|
| Price | $0 | $14/mo ($134/yr) | $59/mo ($566/yr) |
| Apps | 1 | 5 | Unlimited |

Everything else identical to Option A.

**Pros:**
- $14 Pro undercuts every competitor's entry paid tier (Hyperping Hobby $14, Healthchecks Supporter ~$17, Cronitor Developer $20)
- Maximizes conversion from free to paid
- Higher Team price captures more from teams that clearly need it

**Cons:**
- $14 signals "cheap tool" not "professional infrastructure"
- Smaller MRR per customer during the critical early phase
- Harder to raise prices later without upsetting early adopters

### Option C: Higher across the board

| | Free | Pro | Team |
|---|---|---|---|
| Price | $0 | $29/mo ($278/yr) | $79/mo ($758/yr) |
| Apps | 1 | 10 | Unlimited |

**Pros:**
- Higher ARPU from day one
- $29 matches Hyperping Basic, still under Cronitor Business ($50)
- More room for future discounts or promotional pricing

**Cons:**
- Unproven product at $29/mo will struggle to convert against Cronitor ($20 with brand trust) and Healthchecks.io (free for 20 checks)
- No brand recognition to justify premium pricing yet
- Risk of very low conversion that makes it impossible to learn from user behavior

---

## 3. Feature Gating: Free / Pro / Team

This is what should be enforced in PlanLimits and what is already mostly correct in the codebase.

### Free (lead gen + self-serve onboarding)
- 1 app, 5 monitors, 7-day history, 1 member (owner only)
- Dashboard access (view monitors, recent events)
- No alerts (this is the #1 upgrade trigger)
- No API access
- No status pages
- No MCP server access (gated by API key which requires Pro+)

### Pro (solo devs and small teams, primary revenue driver)
- 5 apps, unlimited monitors, 90-day history, 3 members
- All alert channels: Slack, email, PagerDuty, webhook
- REST API access
- 1 status page per app
- MCP server access
- 14-day free trial, no CC required

### Team (agencies, larger engineering teams)
- Unlimited apps, unlimited monitors, 1-year history, unlimited members
- Everything in Pro, plus:
- Custom alert rules (e.g., "only alert if 3 consecutive failures")
- Unlimited status pages
- Priority email support (24h response SLA)
- Future: audit log, SSO/SAML (upsell hooks for later)

### Gating philosophy

The free tier must be **useful enough to prove the product works** but **painful enough that any serious user upgrades within a week.** The key pain points:

1. **No alerts on Free.** A monitoring tool without alerts is a dashboard. Dashboards don't retain users. The moment a cron job fails silently, the user upgrades.
2. **1 app on Free.** Most developers have at least 2 projects (production + staging, or two products). The second app forces the upgrade conversation.
3. **7-day history on Free.** Can't investigate last month's incident without upgrading.

---

## 4. Competitor Positioning

### Pricing landscape (April 2026)

| Competitor | Entry paid price | Model | Cron-specific? | Free tier |
|---|---|---|---|---|
| **Cronitor** | $20/mo (20 monitors) | Per-monitor tiers | Yes, core focus | 5 monitors |
| **Healthchecks.io** | ~$17/mo (Supporter) | Flat tiers by checks | Yes, core focus | 20 checks |
| **Hyperping** | $14/mo (15 monitors) | Flat tiers by monitors | No, uptime focus | 5 monitors |
| **Better Stack** | ~$50/mo (monitors + on-call) | Component add-ons | No, full observability | Yes (limited) |
| **Oh Dear** | ~$15/mo | Flat tiers by sites | No, uptime/SSL/perf focus | No (trial only) |
| **Crontinel** | $19/mo (5 apps, unlimited monitors) | Flat tiers by apps | Yes, Laravel-first | 1 app, 5 monitors |

### Where Crontinel positions

**Below Cronitor and Better Stack. At parity with Healthchecks.io and Oh Dear. Above Hyperping's hobby tier.**

The positioning argument:

- **vs. Cronitor ($20/mo for 20 monitors):** Crontinel gives unlimited monitors for $19/mo. Cronitor charges per monitor, which punishes thorough monitoring. Crontinel is Laravel-native with a Composer package; Cronitor is language-agnostic (broader but shallower integration). Lead with "unlimited monitors, $1 less."

- **vs. Healthchecks.io (free for 20 checks, ~$17/mo paid):** Healthchecks.io is the budget leader and open-source. Crontinel can't win on price here. Win on Laravel-native DX instead: `composer require crontinel/laravel` vs. manual HTTP pings. Healthchecks.io has no framework integration, no Horizon monitoring, no queue awareness.

- **vs. Better Stack (~$50+/mo for comparable features):** Better Stack is a full observability platform (logs, uptime, on-call). It's 2-3x Crontinel's price for the monitoring piece alone. Position Crontinel as the focused, affordable alternative for teams that only need cron/queue monitoring, not a full observability suite.

- **vs. Oh Dear (~$15/mo):** Oh Dear is Laravel-ecosystem friendly (built by Spatie) but focuses on uptime/SSL/broken links, not cron monitoring. Scheduled task monitoring is a secondary feature. Crontinel is purpose-built for crons and queues. Complementary, not competitive.

- **vs. Hyperping ($14-29/mo):** Hyperping focuses on HTTP uptime checks and status pages. Minimal cron monitoring. Not a direct competitor. Crontinel only overlaps on status pages.

### Crontinel's differentiation (what justifies the price)

1. **Laravel-native.** Only monitoring tool that ships a Composer package with auto-discovery, Horizon integration, and queue-aware monitors. Zero-config for Laravel apps.
2. **OSS + SaaS model (Sentry playbook).** Self-host for free, pay for hosted convenience. This builds trust and community that pure-SaaS competitors lack.
3. **MCP server.** AI assistant integration via Claude Code / Cursor. No competitor offers this. Novel, and increasingly relevant as AI-assisted ops grows.
4. **Unlimited monitors on every paid plan.** Cronitor and Hyperping both cap monitors per tier. Crontinel's "add as many monitors as you want" removes friction.

---

## 5. Open Questions

These are the decisions Harun needs to make before finalizing pricing. They do not block launch.

### Must decide before first paying customer

1. **Stripe Price IDs.** Create the actual Stripe products and prices for Pro Monthly ($19), Pro Yearly ($182), Team Monthly ($49), Team Yearly ($470). Wire them into Cashier config. This is implementation, not a pricing decision, but it needs doing.

2. **Trial-to-paid conversion flow.** The trial expires after 14 days and drops to Free. Is there a grace period? A "your trial expired" email sequence? Currently `TrialExpiredMail` exists but the nudge sequence is unclear.

3. **Overage handling.** When a Pro user hits 5 apps, do they see an upgrade prompt, get blocked, or get a soft limit? Current `PlanLimits::canCreateApp()` returns false, which presumably blocks creation. Confirm the UX is clear (not just a silent failure).

### Should decide before public launch

4. **Annual pricing math.** The current yearly prices ($182 Pro, $470 Team) are exactly 20% off. Consider rounding to friendlier numbers: $179/yr Pro ($14.92/mo), $468/yr Team ($39/mo). Or keep it clean. Minor, but affects the FAQ copy.

5. **Upgrade path between Pro and Team.** The jump is $19 to $49 (2.6x). Is there demand for a middle tier (e.g., "Pro Plus" at $29 for 10 apps and 10 members)? Don't add this now. Wait for data. But plan for the possibility in the Stripe product structure.

6. **Status page as upsell.** Free gets 0, Pro gets 1/app, Team gets unlimited. Should status pages be an add-on ($5/mo per page) instead? This creates metered complexity. Recommendation: keep it bundled for now, revisit after 50+ paying customers.

### Can defer until post-launch

7. **Enterprise tier.** "Contact us" pricing for SOC2, SSO/SAML, audit logs, SLA guarantees, dedicated support. Don't build this yet. Add a "Need more?" contact link on the pricing page.

8. **Non-profit / OSS discount.** Healthchecks.io gives Business free to OSS projects. Good for community goodwill but costs nothing at scale. Decide after launch.

9. **Lifetime deal (LTD).** AppSumo or standalone LTD for early traction. High risk of attracting low-quality customers who never convert to recurring. Avoid unless desperate for initial users.

---

## Decision Summary

**Ship with Option A (current pricing: Free $0 / Pro $19 / Team $49).** It is correctly positioned against competitors, already implemented in the codebase and landing page, and appropriate for a new entrant without brand recognition. The pricing can be raised later once there is evidence of willingness to pay. It cannot easily be lowered without upsetting early customers.

The current feature gating in `PlanLimits.php` matches this recommendation. No code changes needed for pricing.

**Next action:** Create Stripe products/prices and wire them into `config/cashier.php`.
