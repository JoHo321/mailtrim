# Privacy Policy

mailtrim is designed to keep your email data under your control.

## What stays local (everything by default)

| Data | Where stored |
|------|-------------|
| OAuth token | `~/.mailtrim/token.json` (mode 0o600) |
| Email metadata cache | `~/.mailtrim/mailtrim.db` (SQLite) |
| Undo logs | `~/.mailtrim/mailtrim.db` |
| Rules & follow-ups | `~/.mailtrim/mailtrim.db` |
| Unsubscribe history | `~/.mailtrim/mailtrim.db` |

**Full email body content is never stored locally or sent anywhere.**

## What leaves your machine

### Gmail API (always)
Every command that reads or modifies email communicates with `googleapis.com` using your OAuth token. This is unavoidable — it's how the Gmail API works.

### Anthropic API (only when ANTHROPIC_API_KEY is set)
When you use `triage`, `bulk`, `rules --add`, `avoid`, or `digest`, the following data is sent to the Anthropic API for AI classification:

| Field | Sent? |
|-------|-------|
| Email subject | Yes |
| Sender name / address | Yes |
| Snippet (first ~200 chars) | Yes |
| Full body (text/HTML) | **No** |
| Attachments | **No** |
| Your email address | **No** |

If you run without `ANTHROPIC_API_KEY`, the MockAIEngine is used — no data leaves your machine for AI purposes.

### Unsubscribe (headless browser)
When `--unsub` is used with Playwright, your machine visits the sender's unsubscribe URL directly. No data passes through mailtrim servers (there are none).

## Revoking access

To fully disconnect mailtrim:

```bash
# 1. Delete the local token
rm ~/.mailtrim/token.json

# 2. Revoke at Google
# https://myaccount.google.com/permissions
# Find "Desktop app" and click "Remove access"
```

## No telemetry

mailtrim contains no analytics, crash reporting, or usage tracking of any kind. It is a local tool that makes API calls only on your explicit command.
