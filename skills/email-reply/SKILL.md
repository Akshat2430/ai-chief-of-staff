---
name: email-reply
description: Draft a reply to an email in Alex's voice — direct, concise, relationship-aware
version: 1.0
author: Alex Johnson
referenced_files:
  - .claude/context/communication-style.md
  - .claude/context/my-team.md
  - .claude/context/my-priorities.md
---

# Email Reply Skill

## What this skill does

Drafts email replies that sound like me — not like a polished AI assistant.
Before writing anything, read `.claude/context/communication-style.md` in full.
Then read `.claude/context/my-team.md` to understand who I'm writing to.

## How to use

The user will provide the email to reply to, either by pasting it or referencing it from triage.
Ask one clarifying question if the intent is ambiguous: "What's the outcome you want from this reply?"
Otherwise, draft immediately.

---

## Drafting instructions

### Step 1 — Identify the relationship

Look up the sender in `.claude/context/my-team.md`.
- Direct report → casual, warm, short
- Manager (Sarah) → structured, proactive, no fluff
- Executive / board → concise, business-first, clear ask
- External partner → warmer opener, professional close
- Hartwell Group → always CC Marcus and Sarah, extra attentive tone
- Unknown external → treat as professional external

### Step 2 — Identify the intent

What does the email want from me?
- A decision → lead my reply with the decision, then reasoning
- An update → give the update first, then context
- A question → answer it directly, don't restate the question
- A complaint / escalation → acknowledge specifically (not generically), state what I'm doing

### Step 3 — Write the draft

Apply ALL of the following:
- Subject line: keep original or improve if it's vague. Use [ACTION NEEDED] / [FYI] prefix where appropriate.
- Opening: no "I hope this finds you well." Start with the substance.
- Body: short. State the point in the first sentence. Use bullets for 3+ items.
- Closing: match the sign-off to the relationship (see communication-style.md).
- Length: aim for under 150 words unless complexity requires more. Flag if you went over.

### Step 4 — Self-check before outputting

Before presenting the draft, silently verify:
- [ ] Does it start with the point, not a preamble?
- [ ] Are there any banned phrases from communication-style.md?
- [ ] Is the tone matched to the relationship type?
- [ ] Is there a clear next step or is it an FYI?
- [ ] Is it shorter than it could be?

If any check fails, revise before showing.

---

## Output format

Present the draft inside a clearly labelled block:

```
To: [recipient]
Subject: [subject]

[draft body]
```

Then offer: "Want me to adjust tone, length, or change the ask?"

Do NOT explain what you did or why. Just produce the draft and offer the adjustment prompt.

---

## Examples of voice

**Too formal (wrong):**
> "I hope this message finds you well. I wanted to follow up on our previous conversation regarding the Orion v2 timeline and provide an update as requested. Please don't hesitate to reach out if you need any additional information."

**Too casual (wrong):**
> "Hey! Just saw your email. Yeah totally, let's do it. Sounds good to me!"

**Right (direct report):**
> "QA update: one critical bug still open (ticket #841), Kai's on it. We're still on track for April 15 but I'll flag if that changes. Anything you need from me today?"

**Right (executive):**
> "We're on track for the Orion v2 launch (April 15). One open QA issue — being resolved this week, doesn't affect timeline. I'll send a full readout by EOW. No action needed from you."

**Right (Hartwell / external):**
> "Thanks for flagging this, James. I've looked into the integration issue you mentioned and here's where we stand: [detail]. We'll have a fix in your environment by Thursday. I'll keep you posted."
