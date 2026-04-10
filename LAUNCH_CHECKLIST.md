# Crontinel Launch Checklist

Groups tasks by phase. Not everything needs to happen on day 1.

---

## Launch day (day 0)

### Community posts
- [ ] Post to r/PHP (approved draft ready at `projects/reddit-marketing/ops/drafts/r-php-launch-DRAFT.md`)
- [ ] Post to r/selfhosted (approved draft ready at `projects/reddit-marketing/ops/drafts/r-selfhosted-launch-DRAFT.md`)
- [ ] Post to r/webdev (approved draft ready at `projects/reddit-marketing/ops/drafts/r-webdev-launch-DRAFT.md`)
- [ ] Post to Dev.to
- [ ] Post to r/laravel (after May 10 cooldown)

### Content / announcements
- [ ] Submit to Product Hunt
- [ ] Post to HN (Show HN if demo-focused, Ask HN if question/discussion)
- [ ] Email launch announcement to waitlist via Resend
- [ ] Share on LinkedIn (if applicable)

### Infrastructure verification
- [ ] Verify Resend domain verified (MX conflict with Zoho must be resolved first)
- [ ] Verify crontinel.com DNS correct
- [ ] Verify app.crontinel.com accessible
- [ ] Verify docs.crontinel.com accessible
- [ ] Verify Gatus status page working (blocked: Hetzner VPS not provisioned)
- [ ] Check error logs for any issues

---

## First week

### Engagement
- [ ] Monitor for feedback on all platforms
- [ ] Reply to all comments within 24 hours
- [ ] DM each new follower / commenter personally

### Product
- [ ] Fix any urgent bugs found by early users
- [ ] Ship at least one improvement based on early feedback

### Analytics / follow-up
- [ ] Check analytics for traffic sources (GA4)
- [ ] Send follow-up email to waitlist (day 3)
- [ ] Identify top 3 acquisition channels, double down

---

## Ongoing

### Distribution
- [ ] Write 1 blog post per week based on what users ask about
- [ ] Engage in Reddit threads organically (BuildBeforeHype account)
- [ ] Target 1 podcast / interview opportunity per month

### Product
- [ ] Add top requested feature within 2 weeks of launch
- [ ] Set up user onboarding survey (Typeform or direct email)
- [ ] Call or video chat with 3 power users in first month

### Business
- [ ] First paying customer — get on a call, learn everything
- [ ] Review pricing at 30 days (too cheap / right / could go higher)
- [ ] Explore partnership opportunities (Laravel partners, hosting companies)

---

## Blockers currently open

- Reddit API: CAPTCHA blocks app registration. Manual setup needed at reddit.com/prefs/apps/
- Resend domain: MX conflict with Zoho prevents verification
- Hetzner VPS: not provisioned yet, Gatus status page on hold
- Cloudflare API key: authentication error 10000, www redirect on hold
- r/laravel: one-month cooldown from subreddit mod notice (reopens May 10, 2026)
