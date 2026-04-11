# Guest Post Pitch: honeybadger.io

**To:** pitches@honeybadger.io (or the submission form at honeybadger.io/blog/write-for-us/)
**Subject:** [Guest Post] Why Your Laravel Cron Jobs Are Failing Silently

---

## Pitch

Hi Honeybadger team,

I'm Harun Rayhan, a Laravel developer building [Crontinel](https://crontinel.com) — a monitoring tool focused specifically on Laravel cron jobs, scheduled tasks, and Horizon queues.

I'd love to write a guest post for the Honeybadger blog. Here's my proposed topic:

**Title:** _Why Your Laravel Cron Jobs Are Failing Silently (And How to Catch It Before Users Notice)_

**Angle:** Laravel developers trust their scheduled tasks, but cron failures are uniquely invisible. Unlike HTTP errors that surface immediately, a broken `send-invoices` cron job will run, fail, and exit with a non-zero code — and nobody will know unless you've built explicit monitoring around it. This post walks through the failure modes, why standard uptime monitors miss them, and how to detect them properly.

**What the post covers:**
1. The three most common ways Laravel cron jobs fail silently (wrong schedule syntax, overlapping jobs, queue worker crashes)
2. Why ping-based uptime monitoring is blind to background job failures
3. A code-first walkthrough of Laravel's scheduler events and queue worker lifecycle hooks
4. How to build a lightweight failure detector using those hooks (with working PHP/Laravel code examples)
5. When to reach for a monitoring tool vs. rolling your own

**Target length:** ~1,800 words
**Audience:** PHP/Laravel developers running production apps
**Tone:** Practical, code-heavy, not promotional — the post solves a real problem and mentions Crontinel only as one option among several

I've linked to Honeybadger in my existing blog content before, and I think this topic fits your audience well. Let me know if you'd like me to submit a full draft.

Thanks for your time,
Harun Rayhan
[@HarunRRayhan](https://x.com/HarunRRayhan) | [crontinel.com](https://crontinel.com)

---

## Notes for Ray

- Honeybadger pays $500 per accepted post (PayPal)
- They explicitly welcome PHP/Laravel content
- Topic naturally complements their error monitoring focus — cron failures are a type of silent error
- The post should NOT be a sales pitch; Honeybadger's editors are strict about this
- Mention Crontinel only in the "tools to consider" section at the end, not as the focus
- Pitch via: https://honeybadger.io/blog/write-for-us/ or the contact form
