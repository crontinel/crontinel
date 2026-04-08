# Crontinel Early Adopter Plan: First 10 Serious Users

Last updated: 2026-04-08

Goal: 10 active users who install crontinel/laravel, connect to the SaaS, and give feedback. Not signups. Not waitlist entries. Real installs with real cron jobs being monitored.

---

## 1. Channel Ranking

Ranked by likelihood of finding Laravel developers who run cron jobs in production and care about reliability.

### Tier A: High-intent, direct access to target users

**1. r/laravel (Reddit)**
Best single channel. Developers here literally post about Horizon stuck states, schedule:run not firing, and queue workers dying after deploys. Pain relevance is 5/5. Account u/BuildBeforeHype is already warming up here. Post format: problem-led "I built this after my nightly sync died for 4 days" story, not a product announcement.

**2. Laravel Discord (discord.gg/laravel, ~70k members)**
The official Laravel Discord has #packages, #help, and #general channels. Package authors hang out here. The approach: answer Horizon/scheduler questions in #help for a week, then share in #packages with a "just shipped this, looking for early testers" message. Direct DMs to people who asked about cron monitoring in the last 30 days.

**3. Laracasts Forum (laracasts.com/discuss)**
Jeffrey Way's community. ~50k active members. People post about production issues, package recommendations, and "how do you handle X" threads. Search for threads mentioning "scheduler," "Horizon," "cron," and "monitoring." Reply with genuine answers, then follow up with the poster via DM or thread reply offering early access.

**4. Direct outreach to Laravel open-source maintainers**
Target: developers who maintain Laravel packages with scheduled tasks, queue jobs, or Horizon integration. They understand the problem viscerally. Find them on GitHub by searching repos that use `$schedule->command()` or `Horizon::`. Send a personal email or DM referencing their specific package. 15-20 targeted messages, expect 3-5 responses.

Specific targets to research:
- Maintainers of spatie/* packages (especially spatie/laravel-backup, which runs scheduled tasks)
- Authors of laravel-medialibrary, laravel-activitylog, or any package with artisan commands
- Developers who contribute to Horizon itself
- Authors of queue-related packages (laravel-horizon-watcher, etc.)

**5. X/Twitter Laravel community**
Search for tweets containing "Laravel cron," "Horizon stuck," "scheduler not running," "queue workers died." The Laravel Twitter community is active and founder-friendly. Taylor Otwell, Freek Van der Herten, Mohamed Said, Nuno Maduro, and their followers are the core audience. A short thread showing "here's what silent cron failure looks like and what I built to fix it" can reach thousands.

Specific accounts to engage with (reply to their content, build visibility before pitching):
- @taylorotwell (Laravel creator)
- @faborsky (Freek, Spatie)
- @themsaid (Mohamed Said, former Laravel team)
- @enunomaduro (Nuno Maduro, Pest/Laravel)
- @christophrumpel
- @marcelpociot (BeyondCode)
- @jbrooksuk (Cachet/Laravel)

Don't cold-DM these people. Reply to their tweets with useful technical takes for 1-2 weeks, then post your own thread.

### Tier B: Good reach, less targeted

**6. r/selfhosted**
Strong for the OSS angle. Frame Crontinel as "self-hosted cron monitoring for Laravel" and link the MIT package. This community respects open-source-first products. Not joining yet per warmup plan; target after day 14.

**7. Indie Hackers (indiehackers.com)**
Good for the "building in public" angle. Post in the Products section and the community forum. The audience is founders, not Laravel developers specifically, so lead with the problem ("how I caught a billing sync that silently failed for 4 days") not the stack. Cross-post the launch post here.

**8. dev.to**
Publish a tutorial: "Monitor your Laravel cron jobs in 5 minutes with Crontinel." Dev.to has strong SEO and the Laravel tag gets decent traffic. This is a slower burn but compounds. Write 2-3 posts: one problem-awareness ("the silent failure problem"), one tutorial ("how to set it up"), one comparison ("Crontinel vs. Cronitor vs. Healthchecks.io for Laravel").

**9. Laravel News (laravel-news.com)**
Submit to their "Laravel Links" section and pitch Eric Barnes directly for a package spotlight. Laravel News is the highest-authority channel in the ecosystem. A mention here is worth 50 Reddit posts. The pitch: "New OSS package for cron/queue/Horizon monitoring with optional SaaS dashboard." They feature new packages regularly.

Contact: submissions@laravel-news.com or DM @ericlbarnes on Twitter.

**10. Show HN (news.ycombinator.com)**
Already in the launch checklist. Title: "Show HN: Crontinel -- Laravel cron job monitoring with Composer package and MCP server." The MCP angle is the differentiator that makes HN care. Time for a weekday morning US Eastern.

### Tier C: Supplementary

**11. r/PHP** -- adjacent audience, less Laravel-specific, good for broader PHP visibility
**12. r/SaaS** -- founder journey posts after account is established (30+ days)
**13. r/sideproject** -- "here's what I built" post with screenshots
**14. r/devops** -- high technical bar, save for after 200+ karma and confident positioning
**15. Packagist trending** -- not a channel you control, but a stable Packagist release with good README and install count snowballs discovery

---

## 2. Early Adopter Offer

### What to offer

**Primary offer: Extended Pro trial (60 days instead of 14) + direct Telegram/email access to the founder.**

Do not do a lifetime deal. The PRICING.md explicitly flags LTDs as high-risk for attracting low-quality customers. Instead:

| Offer element | Details |
|---|---|
| Extended trial | 60-day Pro trial instead of 14. Enough time to see real value across deploy cycles and incident windows. |
| Founder access | Direct Telegram group or email thread. "You can message me when something breaks or when something is confusing." |
| Feature priority | "Tell me what's missing. The first 10 users shape the roadmap." Specific: they can request alert channels, dashboard views, or integrations and see them shipped within days. |
| Name on the wall | Early adopters listed on a future "Built with feedback from" section. Small, but founder-types value recognition. |
| Lock-in pricing | "Whatever price you start at, you keep. If I raise prices later, your rate stays." This is low-risk because prices are more likely to go up than down. |

### What NOT to offer

- No lifetime deal. Attracts deal hunters, not product users.
- No free forever Pro. Undermines the pricing model. The free tier already exists.
- No "use it free and pay later if you want." That's a free tier, which already exists.

### What to ask for

| Ask | Why |
|---|---|
| Install it in a real project with real cron jobs | Synthetic testing tells you nothing. You need production-adjacent usage. |
| Use it for 2 weeks before giving feedback | Day-one feedback is about UI polish. Week-two feedback is about real value. |
| Report every moment of confusion | Onboarding friction is the #1 killer. The ONBOARDING_AUDIT found 5 major friction points already. Real users will find more. |
| Share it with one other Laravel developer if they find it useful | Warm referrals from trusted developers are the highest-converting channel. |
| Be honest about whether they'd pay $19/mo | Willingness-to-pay signal is the most important data point at this stage. |

---

## 3. Ideal Early Adopter Profile

A strong early adopter for Crontinel matches at least 4 of these 6 criteria:

1. **Runs Laravel cron jobs in production today.** Not "planning to" or "has a side project." Actual `schedule:run` in a crontab on a live server. Backup scripts, report generators, billing syncs, data imports, email campaigns.

2. **Has been burned by silent failure.** They have a war story: "my backup hadn't run in 11 days," "our Stripe sync died after a deploy," "Horizon showed active but nothing was processing." This person doesn't need to be convinced the problem is real.

3. **Builds SaaS or client apps (not hobby projects).** The pain has business consequences. A missed cron job means a customer complaint, not just a personal inconvenience. This person will actually pay $19/mo because the cost of failure exceeds the cost of the tool.

4. **Gives specific, actionable feedback.** "It's cool" is useless. "The timezone selector only has 10 options and mine isn't there" is gold. Look for developers who file GitHub issues, contribute to open-source, or write detailed forum posts. Their public history tells you whether they give real feedback.

5. **Has influence in the Laravel community.** Not a requirement, but a multiplier. A developer with 500+ Twitter followers, an active Laracasts profile, or a popular open-source package can amplify Crontinel to their network. One influential early adopter is worth five silent ones.

6. **Not a freebie hunter.** They don't collect free tools. They use tools that solve real problems and are willing to pay for them. Screen for this by asking: "Would you pay $19/mo for this after the trial?" If the answer is hedging, they're not the right fit.

### Red flags (skip these users)

- "I'll try it when I have time" (they won't)
- Only interested in the free tier, no production cron jobs
- Want to self-host everything and philosophically oppose SaaS (point them to the OSS package and move on)
- Ask for features that have nothing to do with cron/queue monitoring (scope creep signal)
- No Laravel projects in production

---

## 4. Outreach Message Templates

### Template 1: DM to a developer who posted about cron/scheduler problems

Use on: Reddit DM, Twitter DM, Discord DM, or email. Triggered by seeing someone post about a relevant problem.

```
Hey [name] -- saw your post about [specific problem, e.g., "Horizon showing active but jobs piling up"]. I've been dealing with the same thing on my own projects.

I'm building a monitoring tool specifically for Laravel cron jobs, queues, and Horizon. It's a Composer package that reports scheduler health to a dashboard with alerts. Still early, looking for Laravel devs who actually run cron in production to test it and tell me what's missing.

If you're interested, I'll set you up with a 60-day Pro trial and you'd have direct access to me for bugs/feedback. No strings, just want honest input from someone who's clearly dealt with this problem.

Either way, for your original issue: [one concrete suggestion related to their problem].
```

Why this works: leads with their specific problem, offers help regardless, positions the ask as lightweight ("tell me what's missing"), and ends with value even if they say no.

### Template 2: Forum/community post (Laracasts, Laravel Discord #packages, dev.to)

```
Title: Looking for early testers -- Laravel cron/queue monitoring package

I've been building Crontinel, a monitoring tool for Laravel scheduled tasks, queues, and Horizon. It's a Composer package (MIT, open source) with an optional SaaS dashboard for alerts and history.

The problem it solves: your health check returns 200 but your nightly backup hasn't run in 5 days. Uptime monitors can't catch that. Crontinel watches whether scheduled tasks actually ran, whether your queue is draining, and whether Horizon workers are healthy.

Install is one command:
composer require crontinel/laravel
php artisan crontinel:install

Looking for 10 Laravel developers who run cron jobs in production and want to try it. You'd get 60 days of Pro (normally 14-day trial) and direct access to me for feedback.

What I need from you: install it on a real project, use it for 2 weeks, tell me every moment of confusion. That's it.

GitHub: github.com/crontinel/crontinel
Docs: docs.crontinel.com

If you're interested, comment here or DM me.
```

Why this works: states the problem concretely, shows the install is simple, makes the ask specific and bounded, and gives both the OSS and SaaS paths.

### Template 3: Cold email to an open-source Laravel maintainer

```
Subject: Quick question about monitoring scheduled tasks in [their package name]

Hey [name],

I use [their package] in a couple of projects and noticed it relies on scheduled tasks for [specific feature, e.g., "cleanup," "pruning," "syncing"]. Quick question: do you monitor whether those tasks actually run in production, or do you rely on users to notice when something breaks?

I ask because I've been building a monitoring tool for exactly this. It's a Laravel package that tracks scheduler health, queue depth, and Horizon worker status. Open source (MIT), with a hosted dashboard option for alerts.

Would love your take on whether this is useful, or whether you've already solved this problem differently. Not trying to sell anything, genuinely want feedback from someone who maintains production Laravel packages.

If you have 10 minutes, I'd set you up with full access and would love to hear what you think.

[name]
crontinel.com
```

Why this works: references their specific work, asks a genuine question, positions the ask as seeking expertise not selling, and respects their time.

### Template 4: r/laravel launch post (for when warmup is complete)

```
Title: I built a Laravel package for monitoring cron jobs, queues, and Horizon -- looking for feedback

After my billing sync cron died silently for 4 days (found out when a customer emailed asking why their invoice was wrong), I built a monitoring tool specifically for Laravel background work.

It's called Crontinel. Two parts:
- OSS Composer package (MIT): monitors your scheduler, queue depth, and Horizon workers. Gives you a local dashboard at /crontinel. Free forever.
- Optional SaaS dashboard: alerts (Slack, email, PagerDuty, webhook), 90-day history, multi-app monitoring.

What it catches that uptime monitors don't:
- Scheduled task that should have run at 2 AM but didn't
- Queue depth growing but no errors in logs
- Horizon showing "active" but workers stuck in reconnect loop
- Workers running old code after a deploy

Setup:
composer require crontinel/laravel
php artisan crontinel:install

That's it. No agents, no sidecars.

Looking for honest feedback, especially from anyone who's been burned by silent cron failures. What am I missing? What would make you actually use this?

GitHub: github.com/crontinel/crontinel
Docs: docs.crontinel.com
```

Why this works: leads with a real story, explains OSS vs SaaS clearly (an issue flagged in ONBOARDING_AUDIT), lists specific failure modes the audience recognizes, and asks for feedback not signups.

---

## 5. Feedback Questions for Early Users

Ask these after 2 weeks of usage. Not a survey. A conversation (Telegram, email, or 15-minute call).

### The 7 questions

**1. "What were you using before Crontinel to monitor your cron jobs?"**
Purpose: understand the competitive landscape from the user's perspective. Common answers will be "nothing," "Healthchecks.io," "a custom health endpoint," or "I check manually." This tells you what you're actually replacing.

**2. "Was there a moment where Crontinel caught something you would have missed?"**
Purpose: validate the core value prop. If the answer is yes, get the full story. These become case studies and social proof. If the answer is no after 2 weeks, the product isn't delivering value fast enough.

**3. "Where did you get confused during setup?"**
Purpose: find onboarding friction beyond what ONBOARDING_AUDIT already identified. Pay attention to: API key copy issues, timezone problems, unclear empty states, "is it working?" uncertainty. Every confusion point is a churn risk.

**4. "What's the first thing you check when you open the dashboard?"**
Purpose: understand which data matters most. If everyone checks queue depth first, make that the hero metric. If nobody looks at Horizon status, maybe it doesn't belong above the fold. This shapes the dashboard layout.

**5. "Would you pay $19/month for this? Why or why not?"**
Purpose: willingness-to-pay validation. Do not accept "maybe" or "probably." Push for specifics: "What would it need to do for you to pay $19?" or "At what price would it be an obvious yes?" If $19 gets consistent pushback, the pricing needs work before scaling.

**6. "What's missing that would make you recommend this to another developer?"**
Purpose: identify the gap between "useful to me" and "worth telling someone about." The answer is usually one specific feature: SMS alerts, a Slack bot, a CLI command, integration with Forge, multi-environment support. This is your roadmap for the next 30 days.

**7. "If Crontinel disappeared tomorrow, what would you do?"**
Purpose: measure dependency. "I'd go back to checking manually" means you've added convenience. "I'd be worried about missing failures" means you've become infrastructure. The second answer means product-market fit is forming.

---

## 6. Execution Timeline

### Week 1-2 (pre-launch, now)

- Finish P0 blockers from LAUNCH_CHECKLIST.md (Packagist release, app.crontinel.com live, waitlist gate removed)
- Continue Reddit warmup (u/BuildBeforeHype, 4-8 comments/week per schedule)
- Join Laravel Discord, start answering questions in #help
- Identify 15-20 open-source maintainers for cold outreach (Template 3)
- Draft the dev.to tutorial post

### Week 3 (launch week)

- Remove waitlist gate, open registration
- Send cold emails to maintainer list (Template 3), expect 3-5 responses
- Post in Laravel Discord #packages (Template 2)
- Post on Laracasts forum (Template 2)
- Post on r/laravel (Template 4, requires user approval per memory rules)
- Submit to Laravel News
- Publish dev.to tutorial
- Post X/Twitter thread

### Week 4-5 (follow-up)

- DM anyone who engaged with launch posts but didn't sign up (Template 1)
- Post Show HN
- Post on Indie Hackers
- Post on r/selfhosted (OSS angle)
- Post on r/sideproject

### Week 6 (feedback collection)

- Conduct feedback conversations with active users (the 7 questions above)
- Prioritize the #1 missing feature from question 6
- Ship it within 1 week
- Share the update with early users: "You asked for X, here it is"

### Success metric

10 users who have:
- Installed crontinel/laravel in a real project
- Connected to app.crontinel.com
- Seen at least one week of monitoring data
- Answered at least 3 of the 7 feedback questions

This is the bar. Waitlist signups, GitHub stars, and Reddit upvotes are vanity metrics until these 10 exist.
