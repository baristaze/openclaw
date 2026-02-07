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
- Browse selected surfaces (per config-template.md, default: Home Following + Explore Trending)
- 1-2 scrolls per surface is sufficient
- Shortlist as soon as good candidates are found
- Track candidates with: URL, author, language, topic, fit reason, engaged-before marker
- Status updates during discovery:
  - "Browsing Home → Following..."
  - "Found N candidates so far..."
  - "Switching to Explore → Trending..."
- Heartbeat: emit "Still working, current step: DISCOVERY" per interval

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
  - total_duration (seconds)
- Include link to posted tweet if applicable
- Status: "Run complete."

---

## Browser Snapshots (token budget)

Always use these params on every `action=snapshot` call:
- `interactive=true` — only interactive elements (buttons, links, inputs)
- `compact=true` — strip layout/decorative nodes
- `maxChars=10000` — cap DOM output at 10K chars

Do NOT set `mode=efficient` (it forces depth=6 which misses Twitter's deep-nested buttons).
Do NOT set `depth` (leave unlimited so like/reply/retweet controls are visible).

---

## Error Handling

Do not retry failed actions. On any browser or page issue:
1. Report the problem to the user with a clear description
2. Wait for user instruction before continuing

This applies to all failures: page loads, clicks, navigation, posting, and any other browser interaction.

---

## Run State Persistence

- Persist current state (lifecycle stage, candidates, selected item)
- On resume: pick up from last completed state
- User can issue "discard run" to abandon and start fresh

## Commands

- `/twitter` — Start new run
- `/twitter resume` — Resume interrupted run
- `/twitter discard` — Discard current run state
