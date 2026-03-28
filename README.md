# AI Chief of Staff

> Built with Claude Code. Commands + Skills + Hooks working as a system.
> From the talk: *"Build Your AI Chief of Staff in 45 Minutes with Claude Code"*

---

## What this is

Most people use Claude Code one feature at a time. This repo shows what happens
when you wire commands, skills, and hooks together into a personal triage and
comms system — one that gets smarter the more context you give it.

**The system does three things:**
1. Runs a daily triage across your email and calendar (`/triage`)
2. Drafts replies that actually sound like you (`email-reply` skill)
3. Logs every triage automatically to build a personal work pattern record (hook)

---

## Repo structure

```
ai-chief-of-staff/
├── .claude/
│   ├── CLAUDE.md                    # Project rules for Claude
│   ├── settings.json                # MCP servers + hook config
│   ├── context/
│   │   ├── my-priorities.md         # Your Q1/Q2 focus areas
│   │   ├── communication-style.md   # Your voice, tone, rules
│   │   └── my-team.md               # Who people are and how to handle them
│   ├── commands/
│   │   └── triage.md                # /triage command
│   └── hooks/
│       └── post-triage-log.sh       # Auto-log hook (runs after Gmail MCP calls)
├── skills/
│   └── email-reply/
│       └── SKILL.md                 # Email reply skill with voice instructions
├── logs/
│   └── .gitkeep                     # weekly-log.md lives here (gitignored)
├── demo/
│   ├── triage-before.md             # What triage looks like with no context
│   ├── triage-after.md              # What triage looks like with context
│   ├── email-draft-before.md        # Generic email draft (no skill)
│   └── email-draft-after.md         # Voice-matched email draft (with skill)
└── setup/
    └── mcp-setup.md                 # Step-by-step Gmail + Calendar MCP setup
```

---

## How it works

### Act 1 — Command + Context

```
/triage
```

Claude pulls your email (Gmail MCP) and calendar (Google Calendar MCP),
reads your three context files, then produces a P0/P1/P2 triage brief.

Without context files: generic summaries, no prioritization.
With context files: knows your stakeholders, your deadlines, your noise filters.

See the difference: [`demo/triage-before.md`](demo/triage-before.md) vs [`demo/triage-after.md`](demo/triage-after.md)

---

### Act 2 — Skill

After triage flags an email:

```
draft a reply to the Hartwell email
```

The `email-reply` skill activates. It reads your `communication-style.md`
and `my-team.md` before writing a single word.

Without skill: polished, generic, full of banned phrases.
With skill: short, direct, sounds like you, correct CCs.

See the difference: [`demo/email-draft-before.md`](demo/email-draft-before.md) vs [`demo/email-draft-after.md`](demo/email-draft-after.md)

---

### Act 3 — Hook

After every triage, a PostToolUse hook fires automatically:

```json
"PostToolUse": [{
  "matcher": "mcp__gmail",
  "hooks": [{ "type": "command", "command": "bash .claude/hooks/post-triage-log.sh" }]
}]
```

This appends a structured entry to `logs/weekly-log.md`. After a month:

```
"Look at my last month of logs. What patterns do you see?
 Where am I spending time that doesn't match my stated priorities?"
```

The system gets smarter the longer you use it.

---

## Quick start

### 1. Clone and open

```bash
git clone https://github.com/Akshat2430/ai-chief-of-staff.git
cd ai-chief-of-staff
claude  # opens Claude Code in this directory
```

### 2. Personalise your context files

Replace the dummy data in these three files with your own:

- [`.claude/context/my-priorities.md`](.claude/context/my-priorities.md) — your Q1/Q2 goals
- [`.claude/context/my-team.md`](.claude/context/my-team.md) — your manager, reports, key stakeholders
- [`.claude/context/communication-style.md`](.claude/context/communication-style.md) — your voice and rules

This is the highest-leverage 20 minutes you'll spend.

### 3. Set up Gmail + Calendar MCPs (optional but recommended)

See [`setup/mcp-setup.md`](setup/mcp-setup.md) for the full guide (~2 minutes).

If you skip this: paste email content manually when running `/triage`.
Everything else — the skill, the hook, the context — still works.

### 4. Run your first triage

```
/triage
```

---

## The system loop

```
Morning                     Afternoon / Evening
   │                               │
/triage                    "Look at my logs.
   │                        What patterns do
   ├── reads context/        you see?"
   │   (priorities,               │
   │    team, style)        weekly-log.md
   │                        → monthly review
   ├── produces brief             │
   │                        → update context
   └── "draft a reply"           files
         │
    email-reply skill        System gets smarter
         │                   every week
    voice-matched draft
```

---

## Updating the system

**Monthly:** Ask Claude to review `logs/weekly-log.md` and compare against `my-priorities.md`. Adjust context files based on what's drifted.

**Quarterly:** Update `my-priorities.md`. The whole system reorients around it automatically.

**When output feels off:** Correct Claude once, then update the relevant context file so you never have to correct it twice.

---

## Talk resources

- Slides: *(link to be added)*
- Demo walkthrough: see the `demo/` folder
- MCP setup: [`setup/mcp-setup.md`](setup/mcp-setup.md)

---

Built by [Akshat Kharbanda](https://www.linkedin.com/in/akshatkharbanda/) · [@akshat2430](https://github.com/Akshat2430)
