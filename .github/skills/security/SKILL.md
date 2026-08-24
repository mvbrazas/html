---
name: security
description: Security checklist for HTML - secrets management, input validation, secure storage, and sensitive data handling.
---

<!-- AUTHORING RULE: Rules and decision tables only. No narrative prose, no rationale, no ticket refs, no future work. Each section answers "what must I do?" -->

# Security - HTML

## When to Activate

- Handling user input or external data
- Working with secrets, tokens, or API keys
- Processing personal or sensitive user data
- Adding new network endpoints or integrations
- Reviewing code for security concerns

## Secrets Management

- Never hardcode secrets, API keys, or credentials in code or config files
- Use environment variables and secure platform configuration
- Rotate any accidentally committed secret immediately
- Keep secret files out of version control

## Input Validation

- Validate all external input at system boundaries
- Validate type, length, format, and range
- Reject invalid input early with explicit error state
- Use allowlists over denylists for permitted values

## Sensitive Data Storage

- Do not store tokens or credentials in plain localStorage/sessionStorage
- Use secure HTTP-only cookie/session mechanisms when auth exists
- Clear sensitive cached data on logout

## Network Security

- Use HTTPS for all external API calls
- Never send secrets in query strings
- Set auth headers only through shared service layers
- Validate backend response shape before use

## Sensitive Data in Responses and UI

- Never render raw internal errors to end users
- Strip sensitive fields before logging or rendering
- Avoid exposing identifiers not required by the UI

## Pre-Commit Security Checklist

- [ ] No hardcoded secrets or credentials
- [ ] Secret files not staged
- [ ] All user inputs validated
- [ ] Sensitive values masked in logs
- [ ] No sensitive data in plain local storage
- [ ] HTTPS used for all external API calls
- [ ] Error UI reveals no internal details
