# Human Approval Workflow (Twitter/X)

Purpose: keep quality high while staying bias-to-action. This workflow defines:
- the two checkpoints (Top-3 shortlist, Final draft)
- message templates
- how to interpret feedback fast
- what to do if the user doesn’t respond within 10 minutes

Default policy:
- Wait up to **10 minutes** at each checkpoint.
- If no response, proceed automatically with the best option (unless user configured “pause on no-response”).

---

## 0) General rules for messaging

Keep messages:
- short
- scannable
- decision-oriented

Always include:
- what you need from the user (choose A/B/C, edits, “go ahead”)
- the timeout and what will happen if they don’t respond

If a channel supports replies/quoting, prefer that for clarity.

---

## 1) Checkpoint A — Top-3 candidate shortlist

### When to send
After discovery and ranking, before drafting the final tweet.

### What to include (each candidate)
For each of the 3:
- Type: Reply / Quote / Original
- Target link + author (if reply/quote)
- 1-sentence angle (the “value add”)
- Why it fits (interests + style + optimization target)
- Risk flag (only if relevant)

### Template: Top-3 shortlist message

**Subject line (first line):**
- “Twitter discovery done — pick 1 (10 min window)”

**Message body:**
- “I found 3 strong options. Reply with **A / B / C**, or tell me what to change.”
- “If you don’t respond in **10 minutes**, I’ll proceed with the best option.”

**Candidates:**
A) **[TYPE]** — @AUTHOR  
Link: <URL>  
Angle: <1 sentence>  
Why: <1 short bullet OR one clause>  
Risk: <None | short note>

B) **[TYPE]** — @AUTHOR  
Link: <URL>  
Angle: <1 sentence>  
Why: <...>  
Risk: <...>

C) **[TYPE]** — @AUTHOR  
Link: <URL>  
Angle: <1 sentence>  
Why: <...>  
Risk: <...>

**Quick knobs (optional, only if helpful):**
- “Prefer: (1) funnier (2) more direct (3) more technical (4) safer”
- “Or: ‘skip today’”

### If the user asks “what would you pick?”
Answer with a firm recommendation:
- pick 1 option + 1–2 reasons tied to the optimization target and persona
- then proceed if approved (or after timeout)

---

## 2) Checkpoint B — Final draft approval

### When to send
After drafting + optimization pass, immediately before posting.

### What to include
- Final draft text exactly as it will be posted
- If reply/quote: target link
- Any optional variants (only if they’re meaningfully different; max 2)
- Ask for: “Approve / Edit / Hold”
- Include the 10-minute timeout behavior

### Template: Final draft message (single draft)

First line:
- “Draft ready — OK to post? (10 min window)”

Body:
Target: <URL> (if reply/quote; otherwise omit)  
Draft:
“<tweet text>”

Reply with:
- “✅ post”
- or edits (paste replacement text)
- or “hold”

No response in **10 minutes**:
- “I’ll post this as-is.” (or “I’ll pause.” if configured)

### Template: Final draft message (two variants)

First line:
- “Draft ready — pick A or B (10 min window)”

Body:
Target: <URL> (if reply/quote)

A)
“<tweet text A>”

B)
“<tweet text B>”

Reply “A” / “B” / edits / “hold”.  
No response in 10 minutes: post **A** (default).

---

## 3) Interpreting user feedback quickly (fast parsing rules)

User feedback usually falls into one of these buckets:

### A) Directional feedback (tone/angle)
Examples:
- “Make it punchier”
- “Less snark”
- “More technical”
- “More playful”
Action:
- revise wording only; keep the core point unless they say to change it.

### B) Content constraints
Examples:
- “Don’t mention X”
- “No links”
- “Avoid @mentions”
- “Don’t engage big accounts”
Action:
- apply constraint immediately and re-run guardrails.

### C) Target selection override (shortlist stage)
Examples:
- “Pick B”
- “Anything but A”
- “None—find something else”
Action:
- if they pick one: proceed
- if “none”: do another discovery pass or pause and ask what to broaden/narrow

### D) Edit-in-place
Examples:
- user pastes rewritten tweet
Action:
- use their text verbatim unless it violates a guardrail; if it does, propose the smallest safe edit and re-ask approval if necessary.

### E) “Hold / pause”
Action:
- do not post; confirm what to do next (wait, redo discovery later, disable auto-post on timeout, etc.).

---

## 4) No-response handling (after 10 minutes)

### Default behavior (bias to action)
If no response within 10 minutes:
- At shortlist stage: pick the highest-ranked candidate and proceed.
- At final draft stage: post the draft as provided.

### If user configured “pause on no-response”
If no response within 10 minutes:
- Do not post.
- Send a short message: “No response—paused. Reply ‘resume’ when ready.”

### If there’s elevated risk
Even with bias-to-action, do **not** auto-post if:
- the topic is sensitive/blacklist-adjacent
- the draft could be misread as hostile
- the thread is chaotic/dogpiley
- there’s uncertainty about login state
In these cases:
- pause and ask for confirmation, or switch to a safer candidate.

---

## 5) Post-confirmation message (optional but recommended)

After posting, send:
- link to the posted tweet
- the final text (optional if link is enough)
- what’s next (e.g., “analytics report will run if enabled”)

Template:
- “Posted ✅ <URL>”
- “Next: I’ll continue low-volume discovery later (or analytics at the next window if enabled).”
