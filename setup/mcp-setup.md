# MCP Setup Guide — Gmail & Google Calendar

You need two MCP servers running for live triage. This guide gets you there.
Estimated time: ~20 minutes.

---

## Step 1 — Create a Google Cloud Project

1. Go to [console.cloud.google.com](https://console.cloud.google.com)
2. Create a new project (e.g. "ai-chief-of-staff")
3. Enable these two APIs:
   - **Gmail API** — search "Gmail API" in the API Library
   - **Google Calendar API** — search "Google Calendar API"

---

## Step 2 — Create OAuth 2.0 Credentials

1. In your project, go to **APIs & Services → Credentials**
2. Click **Create Credentials → OAuth client ID**
3. Application type: **Desktop app**
4. Name it anything (e.g. "Claude MCP Client")
5. Download the JSON — you'll need the `client_id` and `client_secret`

> If prompted to configure a consent screen first: set it to Internal (if using
> Google Workspace) or External with your own email as a test user.

---

## Step 3 — Get a Refresh Token

Run this one-time flow to get your refresh token:

```bash
# Install the Google auth helper
pip install google-auth-oauthlib google-auth-httplib2

# Run the auth flow (replace with your client_id and client_secret)
python3 - <<'EOF'
from google_auth_oauthlib.flow import InstalledAppFlow

SCOPES = [
    'https://www.googleapis.com/auth/gmail.readonly',
    'https://www.googleapis.com/auth/gmail.send',
    'https://www.googleapis.com/auth/calendar.readonly',
]

flow = InstalledAppFlow.from_client_secrets_file('credentials.json', SCOPES)
creds = flow.run_local_server(port=0)

print("CLIENT_ID:", creds.client_id)
print("CLIENT_SECRET:", creds.client_secret)
print("REFRESH_TOKEN:", creds.refresh_token)
EOF
```

Save these values — you'll use them in the next step.

---

## Step 4 — Set Environment Variables

Create a `.env` file in the project root (it's gitignored):

```bash
# .env — never commit this file
GMAIL_CLIENT_ID=your_client_id_here
GMAIL_CLIENT_SECRET=your_client_secret_here
GMAIL_REFRESH_TOKEN=your_refresh_token_here

GOOGLE_CLIENT_ID=your_client_id_here
GOOGLE_CLIENT_SECRET=your_client_secret_here
GOOGLE_REFRESH_TOKEN=your_refresh_token_here
```

> Gmail and Calendar can share the same OAuth client and refresh token
> if you requested both scopes in Step 3.

---

## Step 5 — Install MCP Servers

```bash
# Gmail MCP
npm install -g @gptscript-ai/gmail-mcp-server

# Google Calendar MCP
npm install -g google-calendar-mcp
```

---

## Step 6 — Verify

In Claude Code, run:

```
/mcp
```

You should see `gmail` and `google-calendar` listed as active servers.
Then run `/triage` — it will pull live data.

---

## Troubleshooting

**"MCP server failed to start"**
- Check your env vars are set and the `.env` file is in the project root
- Run the server manually to see the error: `npx @gptscript-ai/gmail-mcp-server`

**"Insufficient permissions"**
- Re-run the auth flow in Step 3 and make sure both Gmail and Calendar scopes are included

**"Token expired"**
- Refresh tokens don't usually expire, but if they do, re-run Step 3

---

## Running without live MCPs

The commands, skills, and hooks all work without live MCPs — you'll just need to
paste email content manually instead of pulling from Gmail. Good for testing the
system before completing OAuth setup.
