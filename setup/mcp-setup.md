# MCP Setup Guide — Gmail & Google Calendar

Claude Code has official Gmail and Google Calendar integrations built in.
Setup takes about 2 minutes.

---

## Connect Gmail

```bash
claude mcp add --transport http gmail https://gmail.mcp.claude.com/mcp
```

A browser window will open — sign in with the Google account you want to triage.
Approve the requested permissions and you're done.

---

## Connect Google Calendar

```bash
claude mcp add --transport http gcal https://gcal.mcp.claude.com/mcp
```

Same flow — browser opens, approve, done.

---

## Verify

Open Claude Code from the project root:

```bash
cd ai-chief-of-staff
claude
```

Run `/mcp` — you should see `gmail` and `gcal` listed as active.

Then run `/triage` to pull live data.

---

## Note

These are Anthropic-hosted official integrations — no Google Cloud project,
no OAuth credentials file, no refresh tokens needed.
