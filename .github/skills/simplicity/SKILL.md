---
name: simplicity
description: Code simplicity rules for HTML - complexity checks, refactoring triggers, and readability standards.
---

<!-- AUTHORING RULE: Rules and decision tables only. No narrative prose, no rationale, no ticket refs, no future work. Each section answers "what must I do?" -->

# Simplicity - HTML

## When to Activate

- Before finalizing any code change
- When a generated solution feels over-engineered
- When a function or component is hard to read in one pass
- When implementing any new feature or fix

## The Primary Rule

**If the generated code is complex, it is wrong. Refactor until it is obvious.**

## Complexity Triggers - Refactor When You See These

| Trigger | Action |
|---------|--------|
| Function/component does more than one thing | Split responsibilities |
| Name contains "and" or "or" | Split behavior |
| Nested `if` / `try` beyond 2 levels | Extract or invert |
| Comment explains what the code does | Rewrite for clarity |
| New abstraction used once | Remove it |
| Utility created for hypothetical future use | Delete it |
| Function exceeds ~30 lines | Find split points |
| New type created for one call site | Inline or simplify |

## Rules

- One function, one responsibility
- Flat over nested - use early returns
- Explicit over clever
- Boring over novel
- No speculative code for hypothetical requirements
- No unnecessary configurability for one use case
- Do not add comments to unchanged code
- Only add comments when the reason is non-obvious

## Async Flow Pattern - Simplicity Check

An async fallback flow must:
- Use sequential, self-contained `try/catch` blocks
- Keep each fallback branch independent
- Avoid generic retry abstractions unless 3+ callers share the pattern

## Before Declaring Work Complete

- [ ] Each function/component does exactly one thing
- [ ] No nested logic beyond 2 levels
- [ ] No single-use abstractions
- [ ] No speculative code
- [ ] Comments explain why, not what
- [ ] A new reader can understand the change in one pass
