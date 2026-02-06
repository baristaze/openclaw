---
name: twitter
description: >
  User-triggered Twitter (X) engagement: discover content, shortlist candidates, draft, approve, post. Manual invocation only.
---

# Twitter Engagement Skill

Single-run, user-triggered workflow:
**STARTED → DISCOVERY → SHORTLIST → DRAFT → APPROVAL → POST/ABORT → FINAL REPORT**

## Defaults

| Parameter | Default | Options |
|-----------|---------|---------|
| Languages | EN, TR | ES, DE, FR, RU, AR, ZH, JA |
| Discovery quota | 30 min, 100 target | — |
| Discovery time cap | 20 min | — |
| Shortlist size | 3 | — |
| Heartbeat interval | 30 sec | — |

## Guardrails

- No DMs
- No following/unfollowing
- Do not reply to mentions unless explicitly instructed
- Never share PII or sensitive info
- Never mention or imply being a bot/AI
- Preserve target content language
- Never engage the same tweet twice (tracked via engagement log)
- Avoid contradicting past posts
- If not logged into X: warn, pause, wait for confirmation

See: `references/safety-guardrails.md`

## Configuration (ask once, reuse)

Collect at start:
1. Interests (whitelist/blacklist topics, accounts)
2. Style/persona constraints
3. Optimization target (impressions/engagement/growth)
4. Approval preference (shortlist + draft, or skip)

Template: `references/config-template.md`

## Supported Actions

- Reply (default, preferred)
- Quote tweet
- Original tweet

Bias: replies > quotes > originals (only originals if clearly superior)

---

## Lifecycle States

### STARTED
- Confirm login state
- Confirm constraints (no DMs, no follow/unfollow)
- Load config (or ask if missing)
- Status: "Run started. Loading config..."

### DISCOVERY
- Browse all 5 surfaces (mandatory coverage):
  - Home: For You, Following
  - Explore: For You, Trending, News
- Quota: minimum items evaluated per defaults
- Track candidates with: URL, author, language, topic, fit reason, engaged-before marker
- Status updates during discovery:
  - "Browsing Home → For You..."
  - "Found N candidates so far..."
  - "Switching to Explore → Trending..."
- Heartbeat: emit "Still working, current step: DISCOVERY" per interval
- Time cap per defaults, but do not shortlist before coverage requirements met

See: `references/discovery-sources.md`

### SHORTLIST
- Select candidates per shortlist size default
- Each candidate includes:
  - Source link
  - Language
  - Type (reply/quote/original)
  - Angle (1 sentence)
  - Risk check (sensitive? note or skip)
  - Reason for selection
- Present to user for selection
- Status: "Shortlist ready. Presenting candidates..."
- Wait for user choice (no auto-proceed)

See: `references/approval-workflow.md`

### DRAFT
- Draft tweet for selected candidate
- Preserve target language
- Apply optimization heuristics
- Final safety scan (no PII, no AI disclosure, no violations)
- Status: "Drafting response..."

See: `references/optimization-heuristics.md`, `references/persona-style-guide.md`

### APPROVAL
- Present draft to user
- Wait for: approve / edit / abort
- No auto-proceed; always wait for explicit user action
- Status: "Draft ready. Awaiting approval..."

### POST or ABORT
- If approved: post and record to engagement log
- If aborted: confirm and end
- Status: "Posted!" or "Run aborted."

### FINAL REPORT
- Emit run summary:
  - tabs_visited (count)
  - items_evaluated (count)
  - shortlisted_items
  - retry_count (browser recovery attempts)
  - resync_count (page state re-syncs)
  - total_duration (seconds)
- Include link to posted tweet if applicable
- Status: "Run complete."

---

## Browser Recovery

When browser stalls or page fails to load:
1. Wait 2 seconds, check if page loaded
2. If not: refresh page
3. If still stuck: close tab, reopen URL
4. If still stuck: report failure, ask user to intervene

After any click/navigation:
- Verify page state changed (not blind waits)
- Detect new-tab scenarios (e.g., external link opens Bloomberg)
- If external site: return to X or notify user

Interaction fallback sequence:
1. DOM click
2. Simulated mouse click
3. Keyboard navigation
4. Direct URL navigation
5. Page refresh

Status updates on retries:
- "Retrying Explore → News click (attempt 2/3, switching to DOM click)"

---

## Run State Persistence

- Persist current state (lifecycle stage, candidates, selected item)
- On resume: pick up from last completed state
- User can issue "discard run" to abandon and start fresh

## Commands

- `/twitter` — Start new run
- `/twitter resume` — Resume interrupted run
- `/twitter discard` — Discard current run state
