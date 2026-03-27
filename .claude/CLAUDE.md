# Chief of Staff — Project Instructions

This project is a personal AI Chief of Staff built on Claude Code.
It uses commands, skills, and hooks together as a system — not one feature at a time.

## How this system works

```
/triage                          # Run morning triage (email + calendar)
  └── reads context/             # Priorities, team, comms style
  └── triggers hook              # Logs triage to weekly-log.md

"draft a reply"                  # After triage flags an email
  └── activates email-reply skill
  └── reads communication-style.md + my-team.md
```

## Key files

| File | Purpose |
|------|---------|
| `.claude/context/my-priorities.md` | What matters this quarter |
| `.claude/context/my-team.md` | Who people are and how to handle them |
| `.claude/context/communication-style.md` | How I write — voice and rules |
| `.claude/commands/triage.md` | The /triage command |
| `skills/email-reply/SKILL.md` | Email drafting skill |
| `.claude/hooks/post-triage-log.sh` | Auto-log hook |
| `logs/weekly-log.md` | Auto-generated, gitignored |

## Updating your context

These files are the system's brain. Keep them current:
- Update `my-priorities.md` each quarter
- Update `my-team.md` when org changes
- Update `communication-style.md` if you correct the output repeatedly

## Rules for Claude in this project

- Always read context files before triaging or drafting
- Never open with "I hope this email finds you well" or any banned phrase from communication-style.md
- Hartwell Group emails always CC Marcus Webb and Sarah Chen
- When in doubt about priority, refer to my-priorities.md
- The weekly log is auto-generated — do not edit it manually
