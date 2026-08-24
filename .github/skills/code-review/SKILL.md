---
name: code-review
description: Code review workflow for HTML. Use for PR reviews, implementation verification, and post-change self-review.
---

# Code Review - HTML

## Context Rule

- If repository context is missing or unclear, read `.github/skills/copilot-instructions.md` before continuing.

## When to Activate

- Reviewing pull requests or diffs
- Verifying implementation against requirements
- Self-review after any code generation or code edits

## Review Rules

- Review only changed files
- Verify UI states for loading, success, empty, and failure
- Validate player input handling and boundary conditions
- Ensure runtime errors are mapped to user-safe overlay or fallback states
- Ensure desktop and mobile rendering remain functional
- Ensure logs mask sensitive data
- Ensure no secrets are hardcoded
- Prefer simple, readable logic over complex abstractions

## Mistake Learning Rule

- If a mistake is identified, stop and classify it as one of: requirement miss, logic bug, validation gap, security gap, UX gap, or process gap.
- Record the concrete trigger that caused the mistake.
- Add or update at least one rule in this skill immediately to block the same mistake pattern.
- Verify the new or updated rule is actionable, testable, and specific.
- Continue work only after the skill update is saved.

## Findings Format

| Severity | File | Line | Finding |
|----------|------|------|---------|
| CRITICAL | | | Security vulnerability, exposed secret, or data-loss risk |
| HIGH | | | Functional bug, missing validation, or crash risk |
| MEDIUM | | | Maintainability issue, stale comment, or inconsistent state handling |
| LOW | | | Naming, consistency, or style issue |
