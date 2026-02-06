# Human Approval Workflow (Twitter/X)

Two checkpoints: Shortlist, Final draft. Both require explicit user action.

---

## 1) General rules for messaging

Keep messages:
- short
- scannable
- decision-oriented

Always include:
- what you need from the user (choose A/B/C, edits, "go ahead")

---

## 2) Checkpoint A — Candidate shortlist

### When to send
After discovery and ranking, before drafting.

### What to include (each candidate)
Per shortlist size in `SKILL.md` defaults:
- Type: Reply / Quote / Original
- Target link + author (if reply/quote)
- Language
- 1-sentence angle (the "value add")
- Why it fits (interests + style + optimization target)
- Risk flag (if relevant)

### Template

**First line:**
"Shortlist ready — pick one"

**Candidates:**
A) **[TYPE]** — @AUTHOR [LANG]
Link: <URL>
Angle: <1 sentence>
Why: <short reason>
Risk: <None | short note>

B) **[TYPE]** — @AUTHOR [LANG]
...

C) **[TYPE]** — @AUTHOR [LANG]
...

**Footer:**
"Reply A / B / C, or 'none' to skip."

### If the user asks "what would you pick?"
Answer with a firm recommendation + 1–2 reasons, then wait for confirmation.

---

## 3) Checkpoint B — Final draft approval

### When to send
After drafting + optimization pass, immediately before posting.

### What to include
- Final draft text exactly as it will be posted
- If reply/quote: target link
- Language note if relevant

### Template (single draft)

**First line:**
"Draft ready — approve, edit, or hold?"

**Body:**
Target: <URL> (if reply/quote)
Draft:
"<tweet text>"

Reply: "post" / edits / "hold"

### Template (two variants)

**First line:**
"Draft ready — pick A or B"

**Body:**
Target: <URL>

A) "<tweet text A>"
B) "<tweet text B>"

Reply "A" / "B" / edits / "hold"

---

## 4) Interpreting user feedback

### A) Directional feedback (tone/angle)
Examples: "Make it punchier", "Less snark", "More technical"
Action: revise wording only; keep core point.

### B) Content constraints
Examples: "Don't mention X", "No links", "Avoid @mentions"
Action: apply constraint, re-run guardrails.

### C) Target selection override
Examples: "Pick B", "Anything but A", "None—find something else"
Action: proceed with pick, or do another discovery pass.

### D) Edit-in-place
Examples: user pastes rewritten tweet
Action: use their text verbatim unless it violates a guardrail.

### E) "Hold / pause"
Action: do not post; confirm what to do next.

---

## 5) Post-confirmation message

After posting, send:
- Link to the posted tweet
- "Posted ✅ <URL>"
