# Crontinel Status Page Feature: Product Scope Document

**Date:** 2026-04-10
**Project:** Crontinel app (HarunRRayhan/crontinel-app)
**Author:** Solo dev planning doc

---

## 1. Gatus Multi-Tenant Analysis

### What Gatus Is

Gatus is a Go-based health check and status page tool. It runs its own HTTP probes against endpoints you define in YAML, stores results in an embedded or external database, and renders a public status page UI. It is designed as a standalone binary with a single config file.

### Multi-Tenant Feasibility

**Single instance, multiple customers: not viable.**

Gatus was built for a single operator monitoring their own infrastructure. The core issues:

- **Configuration is file-based YAML.** There is no API or database-backed config. Adding a new customer's status page means rewriting and reloading YAML. No per-tenant isolation, no per-tenant auth, no per-tenant branding.
- **One status page per instance.** Gatus serves a single `/` status page. There is no concept of "this tenant sees these monitors, that tenant sees those." You would need to fork the UI or proxy/iframe it, which defeats the purpose.
- **No custom domain routing.** Gatus binds to one host:port. Routing `acme.status.crontinel.com` vs `beta.status.crontinel.com` to different tenant views requires a reverse proxy layer you build yourself, plus patching Gatus to filter by tenant.
- **Active probing, not passive ingestion.** Gatus runs its own HTTP/TCP/DNS checks. Crontinel already collects status data from the Laravel SDK. Using Gatus means either (a) duplicating the monitoring by having Gatus also probe endpoints, or (b) writing a custom Gatus storage adapter to read from Crontinel's database. Both are worse than just rendering the data you already have.

**Per-customer deployment: technically possible, operationally painful.**

You could spin up one Gatus container per customer. This means:

- N containers for N customers (memory, CPU, orchestration overhead)
- Dynamic provisioning pipeline (create container, inject config, assign subdomain, TLS cert)
- No shared anything with Crontinel's existing data; you'd need to sync monitor state into each Gatus instance or expose an API Gatus can poll
- Upgrades require rolling N instances

For a solo dev, this is an infrastructure project, not a product feature.

### Verdict on Gatus

**Wrong tool for this job.** Gatus solves a different problem (active probing + status page for a single operator). Crontinel already has the hard part (data collection). The status page is just a read-only view of data that already exists. Building it into the app is strictly simpler.

---

## 2. Building It Into Crontinel Directly

### Why This Is the Right Move

Crontinel already stores everything a status page needs:

- `monitors.status` gives current state (healthy/warning/critical)
- `monitor_events` gives historical state transitions with timestamps
- `active_alerts` gives current open incidents
- `cron_runs` gives recent execution history

A status page is a public, read-only, branded view of this data. No new data collection required.

### New Database Tables

**`status_pages` table:**

```php
Schema::create('status_pages', function (Blueprint $table) {
    $table->id();
    $table->foreignId('app_id')->constrained()->cascadeOnDelete();
    $table->string('slug')->unique();           // used in URL: crontinel.com/status/{slug}
    $table->string('custom_domain')->nullable()->unique(); // status.acme.com
    $table->string('title');                     // "Acme Corp Status"
    $table->text('description')->nullable();
    $table->string('logo_url')->nullable();
    $table->json('theme')->nullable();           // {"primary_color": "#2563eb", "dark_mode": false}
    $table->boolean('is_public')->default(true);
    $table->boolean('show_uptime')->default(true);
    $table->boolean('show_response_time')->default(false);
    $table->boolean('show_branding')->default(true);  // "Monitored by Crontinel" footer badge
    $table->integer('history_days')->default(90);
    $table->timestamps();
});
```

**`status_page_monitors` pivot table:**

```php
Schema::create('status_page_monitors', function (Blueprint $table) {
    $table->id();
    $table->foreignId('status_page_id')->constrained()->cascadeOnDelete();
    $table->foreignId('monitor_id')->constrained()->cascadeOnDelete();
    $table->string('display_name')->nullable();  // override monitor name for public display
    $table->string('group')->nullable();         // "API", "Workers", "Scheduled Tasks"
    $table->integer('sort_order')->default(0);
    $table->timestamps();

    $table->unique(['status_page_id', 'monitor_id']);
});
```

**`status_page_incidents` table (optional for MVP, but cheap to add):**

```php
Schema::create('status_page_incidents', function (Blueprint $table) {
    $table->id();
    $table->foreignId('status_page_id')->constrained()->cascadeOnDelete();
    $table->string('title');
    $table->text('body');                        // markdown
    $table->string('status');                    // investigating, identified, monitoring, resolved
    $table->string('severity');                  // minor, major, critical
    $table->timestamp('started_at');
    $table->timestamp('resolved_at')->nullable();
    $table->timestamps();
});
```

That last table lets customers post manual incident updates ("We are investigating elevated error rates") beyond what automatic monitor status shows.

### Computing Uptime From Existing Data

The `monitor_events` table already records severity transitions. Uptime percentage for a given monitor over N days:

```php
public function computeUptime(Monitor $monitor, int $days = 90): float
{
    $since = now()->subDays($days);
    $totalSeconds = $days * 86400;

    // Get all events in the window, ordered by time
    $events = $monitor->events()
        ->where('occurred_at', '>=', $since)
        ->orderBy('occurred_at')
        ->get(['severity', 'occurred_at']);

    $downtimeSeconds = 0;
    $downSince = null;

    foreach ($events as $event) {
        if ($event->severity === 'critical' && $downSince === null) {
            $downSince = $event->occurred_at;
        } elseif ($event->severity === 'resolved' && $downSince !== null) {
            $downtimeSeconds += $event->occurred_at->diffInSeconds($downSince);
            $downSince = null;
        }
    }

    // If still down, count until now
    if ($downSince !== null) {
        $downtimeSeconds += now()->diffInSeconds($downSince);
    }

    return round((($totalSeconds - $downtimeSeconds) / $totalSeconds) * 100, 3);
}
```

This gives you the classic "99.95% uptime in the last 90 days" number. You can also break it into daily buckets for a 90-day bar chart (green/yellow/red per day).

### Current Status Per Monitor

Already exists: `monitors.status` column. Map directly:

| `monitors.status` | Status page display | Color  |
|---|---|---|
| healthy | Operational | Green |
| warning | Degraded Performance | Yellow |
| critical | Major Outage | Red |
| unknown | Under Maintenance | Gray |

### Route Structure

```php
// Public status page (no auth)
Route::get('/status/{slug}', [StatusPageController::class, 'show'])
    ->name('status.show');

// API for status page (for optional JS polling)
Route::get('/api/status/{slug}', [StatusPageController::class, 'api'])
    ->name('status.api');

// Dashboard management (auth required)
Route::middleware(['auth', 'verified'])->group(function () {
    Route::resource('apps.status-pages', StatusPageManagementController::class)
        ->except(['show']);
});
```

For custom domains, add middleware that checks the `Host` header against `status_pages.custom_domain`:

```php
class ResolveStatusPageDomain
{
    public function handle(Request $request, Closure $next)
    {
        $host = $request->getHost();

        // Skip if it's the main app domain
        if ($host === config('app.domain')) {
            return $next($request);
        }

        $statusPage = StatusPage::where('custom_domain', $host)->first();

        if ($statusPage) {
            return app(StatusPageController::class)->show($statusPage->slug);
        }

        abort(404);
    }
}
```

---

## 3. Product Decision Points

### URL Strategy

**Three tiers of complexity:**

| Approach | Example | TLS | DNS | Effort |
|---|---|---|---|---|
| Path-based | `app.crontinel.com/status/acme` | Zero (existing cert) | Zero | Trivial |
| Subdomain | `acme.status.crontinel.com` | Wildcard cert on `*.status.crontinel.com` | Wildcard DNS A record | Low |
| Custom domain | `status.acme.com` | Per-domain cert via Let's Encrypt or Caddy | Customer adds CNAME | Medium |

**Recommendation for MVP:** Start with path-based (`app.crontinel.com/status/{slug}`). It requires zero infrastructure changes. Add subdomain support in v1.1 (one wildcard cert, one DNS record). Custom domains are a v2 feature, best handled with Caddy or a Cloudflare for SaaS setup.

The path-based approach has one downside: the URL looks like "your monitoring tool" rather than "our status page." But for MVP, shipping fast matters more than vanity URLs.

### UI Approach

**Simple traffic-light vs detailed history:**

For MVP, do both but keep it minimal:

1. **Overall status banner** at the top: "All Systems Operational" (green), "Partial Outage" (yellow), "Major Outage" (red). Derived from the worst status among included monitors.

2. **Per-monitor row** showing: name, current status dot, 90-day uptime bar (one thin rectangle per day, colored by that day's worst status). This is the pattern Atlassian Statuspage and Betterstack use. It is information-dense but visually simple.

3. **Recent incidents** section at the bottom, pulled from `status_page_incidents` or auto-generated from `monitor_events` with critical severity.

Skip: response time graphs, subscriber notifications, embedded status badges, RSS feeds. All are nice-to-haves for later.

### Plan Tier

This feature has near-zero marginal cost per customer (it is a read-only view of existing data). Suggested approach:

- **Free plan:** 1 status page, path-based URL only, Crontinel branding in footer
- **Pro plan:** Unlimited status pages, subdomain URL, custom branding (logo, colors), remove Crontinel branding
- **Business plan:** Custom domain support, incident management, subscriber notifications (future)

The free tier acts as marketing. Every public status page links back to Crontinel.

---

## 4. Effort Estimates

### Option A: Gatus Multi-Tenant

| Task | Hours |
|---|---|
| Research Gatus internals, determine extension points | 4 |
| Build per-tenant config generation pipeline | 8 |
| Container orchestration (Docker Compose or K8s) for N instances | 12 |
| Reverse proxy + TLS for per-customer routing | 8 |
| Sync Crontinel monitor data into Gatus (custom storage or API bridge) | 12 |
| Testing, edge cases, cleanup | 8 |
| **Total** | **~52 hours** |

And you end up maintaining a Go dependency you do not control, with an architecture that fights against the tool's design.

### Option B: Build Into Crontinel

| Task | Hours |
|---|---|
| Migrations (3 tables) | 1 |
| Models, relationships, uptime computation service | 3 |
| Status page public controller + Blade view | 4 |
| Dashboard UI for managing status pages (CRUD, monitor selection) | 6 |
| Custom domain middleware (post-MVP but include the column now) | 2 |
| Styling the public page (responsive, dark/light theme) | 3 |
| Manual incident CRUD in dashboard | 3 |
| Tests | 3 |
| **Total** | **~25 hours** |

### Recommendation

Build it into Crontinel. Half the effort, no external dependency, uses data you already collect, and the result is a tighter product (one less thing for customers to set up). Gatus adds complexity with no offsetting benefit when you already have the monitoring data.

---

## 5. Proposed MVP Spec

### What the Minimal Status Page Shows

1. **Header:** customizable title, optional logo, optional description
2. **Overall status banner:** worst-case status across all included monitors
3. **Monitor list grouped by category:** each row shows display name, status dot (green/yellow/red/gray), 90-day history bar
4. **Uptime percentage** next to each monitor (e.g., "99.97%")
5. **Recent incidents:** last 5 incidents from `status_page_incidents`, showing title, status, and timestamps
6. **Footer:** "Powered by Crontinel" (removable on Pro)

### Migrations Needed

Three migrations as described in Section 2:

1. `create_status_pages_table`
2. `create_status_page_monitors_table`
3. `create_status_page_incidents_table`

### Route Structure

```
GET  /status/{slug}                    -- public status page (Blade)
GET  /api/status/{slug}                -- JSON endpoint for polling
GET  /app/{app}/status-pages           -- dashboard: list status pages
GET  /app/{app}/status-pages/create    -- dashboard: create form
POST /app/{app}/status-pages           -- dashboard: store
GET  /app/{app}/status-pages/{id}/edit -- dashboard: edit form
PUT  /app/{app}/status-pages/{id}      -- dashboard: update
DELETE /app/{app}/status-pages/{id}    -- dashboard: delete
```

### Frontend Approach

**Public status page: server-rendered Blade template.**

Reasons:

- Status pages are read-heavy, write-never (from the visitor's perspective). SSR is ideal.
- SEO matters if customers link to their status page from docs or incident communications. Blade renders instantly with no JS dependency.
- A single Blade view with Tailwind CSS keeps the stack uniform with the rest of Crontinel.
- For live updates, add a small Alpine.js snippet that polls `/api/status/{slug}` every 30 seconds and swaps status dots. No SPA framework needed.

**Dashboard management UI: whatever Crontinel's dashboard already uses.** If it is Livewire or Inertia, follow that pattern. The status page CRUD is standard form-based UI, nothing exotic.

### Key Files to Create

```
app/Models/StatusPage.php
app/Models/StatusPageMonitor.php
app/Models/StatusPageIncident.php
app/Services/UptimeCalculator.php
app/Http/Controllers/StatusPageController.php
app/Http/Controllers/Dashboard/StatusPageManagementController.php
resources/views/status-page/show.blade.php
database/migrations/xxxx_create_status_pages_table.php
database/migrations/xxxx_create_status_page_monitors_table.php
database/migrations/xxxx_create_status_page_incidents_table.php
```

### What Is Explicitly Out of Scope for MVP

- Subdomain or custom domain routing (column exists, middleware deferred)
- Email/SMS/Slack subscriber notifications
- Scheduled maintenance windows
- Embeddable status badge (img/svg)
- RSS/Atom feed of incidents
- Response time graphs
- Status page password protection
- Multi-language support

All of these are straightforward to add later without schema changes (the `settings` JSON column on `status_pages` can absorb most toggle-based features).

---

## Summary

Skip Gatus. Build a simple public Blade view on top of existing Crontinel data. Three new tables, one public controller, one Blade template, roughly 25 hours of work. Ship path-based URLs first (`/status/{slug}`), gate custom domains and branding behind paid tiers. The free tier status page doubles as a marketing channel for Crontinel.
