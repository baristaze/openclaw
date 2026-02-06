# Analytics Reporting (Twitter/X)

Purpose: lightweight performance feedback loops without turning the system into a “dashboard project.”
Reporting is optional and must respect a strict local-time window.

---

## 1) Reporting schedule (strict window)

If analytics reporting is enabled:

- Cadence: **every 3 hours**
- Window: **10:00–22:00 local time** (inclusive start, exclusive end)
  - Allowed report times: 10:00, 13:00, 16:00, 19:00 (and optionally 22:00 only if explicitly requested; default: stop before 22:00)
- Outside the window: **do not send reports**.

If a report is “due” outside the window:
- Skip it (do not catch up overnight).
- Resume at the next valid time within the window.

Local time:
- Use the user’s local timezone if known; otherwise ask once and reuse.
- If timezone is ambiguous, pause reporting until clarified.

---

## 2) What to report (only what’s visible)

Only report metrics that are directly visible in the UI at the time of reporting.
Do not infer, estimate, scrape private endpoints, or claim access to unavailable analytics.

Acceptable metrics (include only if visible):
- Views / impressions (if shown)
- Likes
- Replies
- Reposts / retweets
- Bookmarks (if shown)
- Quote tweets count (if shown)

Also acceptable:
- Timestamp of the tweet (local time)
- Link to the tweet
- Type: reply / quote / original

Not acceptable:
- Follower counts (unless visible and explicitly requested)
- Demographic breakdowns
- “Shadowban” or ranking claims
- Any analytics behind private dashboards unless the user explicitly confirms it is visible and accessible

---

## 3) Which tweets to include

Default: include tweets posted **since the last report** (or within the current day).
If that is unclear, choose the smallest useful scope:
- Up to **5 most recent** tweets max per report (keep it low-noise)
- Always include the most recent post if there is one

If no tweets were posted since the last report:
- Send nothing by default (avoid spam)
- If the user asked for “heartbeat-style” reports regardless, send a single line: “No new posts since last report.”

---

## 4) Reporting format (copy/paste template)

Keep the report short and scannable.

### Template: Analytics Report

**X analytics (local time: <TIME>)**
Scope: <since last report | today | last N tweets>

1) <TYPE> — <tweet link>
- Views: <# | n/a>
- Likes: <# | n/a> · Replies: <# | n/a> · Reposts: <# | n/a> · Bookmarks: <# | n/a>
- Quick read: <1 short sentence>

2) ...

**What I’d try next (1–3 bullets)**
- <bullet>
- <bullet>

Rules:
- Use `n/a` for any metric not visible.
- “Quick read” must be grounded (e.g., “Short + clear hook performed better than yesterday’s longer post.”), not speculation.

---

## 5) Lightweight interpretation heuristics (non-fragile)

When adding “Quick read” / “What I’d try next”:
- Compare *within our own recent posts*, not against universal benchmarks.
- Look for obvious patterns:
  - shorter vs longer
  - reply vs original
  - link vs no-link
  - technical specificity vs generic phrasing
- Avoid grand claims about algorithm changes.

If results are too sparse/noisy:
- Say so (“Small sample; treat as weak signal.”)
- Recommend keeping consistent for another cycle.

---

## 6) Pause / resume behavior (clean controls)

### User commands (plain language)
Treat these as explicit instructions:
- “pause analytics”
- “stop analytics”
- “turn off reporting”
→ Disable analytics reporting immediately. Confirm: “Analytics reporting paused.”

- “resume analytics”
- “turn reporting back on”
→ Re-enable analytics reporting. Confirm next scheduled report time inside the 10:00–22:00 window.

- “report now”
→ Only send a report if current local time is within the allowed window.
If outside: respond with the next scheduled window time.

### Safety on pause/resume
If timezone is unknown or login state is uncertain:
- Pause reporting and ask the user to confirm/fix.
- Do not send partial or misleading reports.

---

## 7) Failure modes

If metrics are not visible (UI changes, not logged in, permissions):
- Report: “Metrics not visible right now; reporting paused until visible again.”
- Ask the user to confirm login / accessibility.

If the channel is noisy:
- Offer to reduce report frequency or limit to the single latest tweet (but keep the default schedule if the user requested it).
