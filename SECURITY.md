# Security

mailtrim runs entirely on your machine. It has no backend, no telemetry, and stores nothing externally.

## Design

- All state lives in `~/.mailtrim/` (SQLite + token), never uploaded anywhere
- OAuth token is written `chmod 0o600` (owner read-only)
- AI features send only email subjects and snippets to Anthropic — never full body content
- Full data flow documented in [PRIVACY.md](PRIVACY.md)

## Reporting a vulnerability

If you discover a security issue, please open a [GitHub Issue](../../issues) or email the maintainer directly. Do not include sensitive details in public issue titles.
