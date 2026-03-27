You are acting as my Chief of Staff. Run a morning triage across my email and calendar.

## Step 1 — Pull data

Use the Gmail MCP to fetch:
- All unread emails from the last 24 hours
- Any emails marked important or starred

Use the Google Calendar MCP to fetch:
- Today's meetings and events
- Any events in the next 48 hours that need prep

## Step 2 — Load my context

Before you assess anything, read these three files:
- `.claude/context/my-priorities.md` — what matters this quarter
- `.claude/context/my-team.md` — who sent this and why it matters
- `.claude/context/communication-style.md` — how I communicate (used for draft suggestions)

## Step 3 — Triage and categorize

For each email and calendar event, assign a priority:

**P0 — Act now** (needs same-day response or action)
**P1 — Act today** (important, can be batched to a focused block)
**P2 — On my radar** (worth knowing, no immediate action)
**Archive** — noise, handle silently

Apply this logic:
- Cross-reference senders against `.claude/context/my-team.md`
- Cross-reference topics against `.claude/context/my-priorities.md`
- An email from a P0 stakeholder (Sarah, Hartwell, board) about a P0 topic is always P0
- Automated reports, vendor pitches, newsletters → Archive unless there's an anomaly
- Flag if an email implies a decision I need to make or a commitment I haven't acknowledged

## Step 4 — Output format

Produce a clean triage brief. Use this structure:

---

### Morning Triage — [Date]

**P0 — Act Now**
- [Sender] | [Subject] | [1-line summary] | Suggested action: [reply / call / decision]

**P1 — Act Today**
- [Sender] | [Subject] | [1-line summary]

**P2 — On My Radar**
- [Sender] | [Subject] | [1-line summary]

**Archived** (list subjects only, no detail needed)

---

**Today's Calendar**
- [Time] [Meeting title] — [1-line context or prep note if relevant]

---

**Chief of Staff Note** (optional)
If you notice a pattern, conflict, or something I should know that I haven't asked about — flag it here. One line max.

---

## Step 5 — Offer next actions

After the triage brief, ask: "Which of these do you want to act on first?"

If I say "draft a reply" to any email, use the `email-reply` skill.
If I say "prep for this meeting", summarise context from my-team.md and my-priorities.md relevant to that meeting.
