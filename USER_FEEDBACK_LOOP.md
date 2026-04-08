# Crontinel — User Feedback Loop

A lightweight, repeatable process for collecting direct user feedback and turning it into product decisions. No automation, no survey tools required — just structured conversations and a simple capture format.

---

## Who to Talk To

### Tier 1 — Highest Signal (talk to first)

- **Early waitlist signups** who answered the "what's your biggest pain with background job monitoring?" question
- **OSS package installers** who opened GitHub issues or discussions (even if resolved)
- **Laravel devs who replied** to your tweets, Reddit posts, or blog comments about Crontinel

These people already have the problem and know who you are. Zero cold-start friction.

### Tier 2 — Warm Outreach

- Laravel Horizon users in communities (Laracasts Discord, r/laravel, Laravel News Discord)
- Indie hackers running Laravel apps in production (look for people posting about queue issues)
- Devs at small agencies who manage multiple client apps

Filter: they must be running Laravel in production. Hobbyists give misleading signal.

### Tier 3 — Competitive Research

- Users of Cronitor, Healthchecks.io, Better Stack who mention frustrations
- Devs who posted about silent cron failures or queue backlog problems (search GitHub issues, Reddit, Twitter)

Use for problem validation only, not feature requests.

---

## What to Ask

### Opening (1 question, sets the stage)

> "Walk me through the last time a background job failed in production and you didn't know right away. What happened?"

This gets a story, not an abstract answer. Listen for: how they found out, how long it took, what the impact was.

### Core questions (pick 3–4 per session, not all)

**Problem depth:**
- "How do you currently monitor your queues and crons? What do you check first when something feels wrong?"
- "Have you ever had a queue silently back up? How did you discover it?"
- "How often do you check Horizon manually? What are you looking for?"

**Current tools:**
- "What monitoring tools are you using today? What do they catch? What do they miss?"
- "Have you tried Cronitor, Healthchecks, or Better Stack? What made you keep or drop them?"

**Decision-making:**
- "If you got an alert that your email queue depth hit 500 jobs — what would you do first?"
- "Would you pay for this today? What would make you say yes immediately vs. 'maybe later'?"

**Crontinel-specific (after you've shown the product):**
- "What's the first thing you'd configure on day one?"
- "What's missing that would make this a must-have instead of nice-to-have?"
- "Is there anything here that feels like it's solving a problem you don't actually have?"

### Closing (always ask this)

> "Who else should I talk to? Anyone in your team or network who deals with this?"

---

## Session Format

**Target:** 20–30 minutes per session. Video call or async text.

**Before the call:**
- Review what they've done (GitHub activity, their app, what they signed up with)
- Note 2–3 specific things to probe based on their context

**During:**
- Record with permission (Loom for async, or note-taking only if live)
- Don't pitch. Don't explain features unless they ask. Just listen.
- When they say something surprising: "Tell me more about that."
- When they describe a workflow: "How often does that happen? Walk me through an example."

**After:**
- Fill out the capture template below within 1 hour while it's fresh
- Tag it with the themes from the taxonomy below

---

## Feedback Capture Template

Save one file per session in `research/feedback/YYYY-MM-DD-<handle>.md`:

```markdown
# Feedback Session — @<handle>
Date: YYYY-MM-DD
Format: [video / async text / DM]
Their context: [company size, # Laravel apps, queue setup, current tools]

## Key quotes
> "[exact quote]"
> "[exact quote]"

## Pain points mentioned (ranked by how emotional they were)
1.
2.
3.

## Current workarounds
-

## What they'd pay for
-

## What they said was missing
-

## Surprises / things I didn't expect
-

## Tags
[queue-depth] [silent-failure] [horizon-specific] [multi-app] [pricing] [onboarding] [alerts]
```

---

## Feedback Taxonomy (tags)

Use consistent tags to spot patterns across sessions:

| Tag | Use when they mention... |
|-----|--------------------------|
| `silent-failure` | Jobs failing without notification |
| `queue-depth` | Backlog accumulation, depth thresholds |
| `horizon-specific` | Horizon supervisor/worker state |
| `cron-miss` | Scheduled commands not running or running late |
| `multi-app` | Managing multiple apps from one place |
| `alerts` | How/where they want to be notified |
| `onboarding` | Install friction, first-run experience |
| `pricing` | Willingness to pay, price sensitivity |
| `competitor` | Comparing to Cronitor, Healthchecks, Better Stack |
| `self-host` | OSS package preference over SaaS |
| `false-positive` | Getting alerted too often / noise |

---

## Turning Feedback Into Product Decisions

After every 5 sessions, do a synthesis review:

### Step 1 — Count tag frequency
List all tags and how many sessions mentioned them. Anything appearing in 3+ sessions is a pattern.

### Step 2 — Quote clustering
Group quotes by theme. If 4 people said something like "I don't know which supervisor is down" in different words — that's a product gap.

### Step 3 — Apply the decision filter

For each pattern, ask:
1. **Is this already in the PRD?** → If yes, reprioritize. If no, add it.
2. **Does it change any current priority?** → Move that item up/down in the milestone.
3. **Does it invalidate a feature we're building?** → Kill it or reshape it.

### Step 4 — Write a one-paragraph decision

For each change you make to the PRD or backlog as a result of feedback, write:
```
Decision [DATE]: Based on [N] user conversations, we [changed X to Y].
Evidence: [1-2 key quotes].
Impact: [what feature or priority this affects].
```

Log this in `research/feedback/DECISIONS.md`.

---

## Cadence

| Activity | Frequency |
|----------|-----------|
| 1:1 feedback session | 2–3/week during early access |
| Synthesis review | After every 5 sessions |
| PRD update based on feedback | As needed, same day as synthesis |
| Share patterns with yourself (review) | Weekly |

Do not batch feedback collection and then do a big synthesis. Do it in small rounds so you can adjust what you're asking based on what you're learning.

---

## Red Flags (signal that feedback is low-quality)

- The person doesn't run Laravel in production → skip or heavily discount
- They're describing hypothetical pain ("I imagine that...") → note but don't weight
- They want features that would make Crontinel a generic APM → that's scope creep
- They only give positive feedback with no friction → push harder with "what would make you stop using it?"
