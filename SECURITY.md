# Security Policy

## Supported Versions

SHAQ MCP Server is a hosted service. The current production version always receives security updates.

| Version | Supported          |
| ------- | ------------------ |
| 1.0.x   | :white_check_mark: |
| < 1.0   | :x:                |

## Reporting a Vulnerability

If you discover a security vulnerability in SHAQ MCP Server, please report it responsibly:

1. **Do NOT open a public GitHub issue.**
2. Email **ayang@shaq-log.com** with:
   - Description of the vulnerability
   - Steps to reproduce
   - Potential impact
   - Suggested fix (if any)
3. You will receive an acknowledgment within 48 hours.
4. We will work with you to validate and remediate the issue.

## Security Measures

SHAQ MCP Server implements the following security practices:

- **No authentication required** — the SSE endpoint is publicly accessible for AI assistants
- **Carrier names are not exposed** — rate results omit carrier identifiers (privacy by design)
- **Bookings are quarantined** — all `create_booking` submissions default to `pending_review`
- **Rate limiting** — API endpoints are rate-limited via nginx
- **HTTPS only** — all endpoints served over TLS
- **No PII stored on server** — bookings contain only operational fields (no payment info)

## Disclosure Timeline

- **Day 0**: Vulnerability reported
- **Day 1**: Acknowledgment sent
- **Day 7**: Initial assessment shared with reporter
- **Day 30**: Fix deployed (or ETA communicated)
- **Day 90**: Public disclosure (after fix is verified)
