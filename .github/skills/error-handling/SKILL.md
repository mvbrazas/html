---
name: error-handling
description: Error handling patterns for HTML - error types, runtime handling, and user-safe fallback responses.
---

<!-- AUTHORING RULE: Rules and decision tables only. No narrative prose, no rationale, no ticket refs, no future work. Each section answers "what must I do?" -->

# Error Handling - HTML

## When to Activate

- Adding or modifying error handling
- Reviewing user-visible failure states
- Handling external service failures

## Rules

- Catch and handle - never swallow errors silently
- Never expose stack traces, raw upstream payloads, or internal messages to users
- Map failures to user-safe overlay or fallback messages in the game UI
- Log errors with structured context: operation name, state name, relevant IDs
- Retry transient failures only when operation is idempotent
- Never retry validation or auth failures

## Failure Categories

| Category | Handling |
|--------|------|
| Validation failure | Ignore invalid action and keep current safe state |
| Asset load failure | Use fallback visuals and continue gameplay |
| Network timeout/offline | Show retry UI and offline-safe message |
| Not found | Show empty/missing state |
| Unexpected failure | Show generic fallback and capture diagnostics |

## External Service Failures

- Never propagate raw upstream error messages to the UI
- Log full error object at error level with external service name
- Normalize external failures into consistent app-level error types
