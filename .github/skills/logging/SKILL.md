---
name: logging
description: Structured logging conventions for HTML - levels, context fields, and sensitive-data masking.
---

<!-- AUTHORING RULE: Rules and decision tables only. No narrative prose, no rationale, no ticket refs, no future work. Each section answers "what must I do?" -->

# Logging - HTML

## When to Activate

- Adding or modifying log statements
- Reviewing code for sensitive data exposure
- Debugging runtime behavior

## Log Levels

| Level | When |
|-------|------|
| `error` | Operation failed and user flow is impacted |
| `warn` | Unexpected condition handled by fallback |
| `info` | Significant user or business event |
| `debug` | Development detail not needed in production |

## Rules

- Use structured fields; avoid unstructured string dumps
- Include game state/feature context and correlation ID when available
- Log errors with full error objects, not only `.message`
- Never log full request/response payloads in production
- Log external asset/service load duration and status

## Sensitive Data - Must Mask Before Logging

| Data Type | Action |
|-----------|--------|
| Email address | Mask |
| Phone number | Mask - last 4 digits only |
| Auth token / JWT | Mask or omit entirely |
| Password | Never log - use `[REDACTED]` |
| Full name | Mask or omit |
| User ID | Partial mask |
| Device identifiers | Partial mask |

## What Not to Log

- Raw API keys or credentials
- Full auth tokens or refresh tokens
- Full PII payloads
- Full local storage snapshots
- Internal stack traces in user-visible UI
