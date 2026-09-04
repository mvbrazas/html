---
name: documentation
description: Standards for writing requirement docs, code review docs, migration reports, and project documentation for HTML.
---

<!-- AUTHORING RULE: Rules and decision tables only. No narrative prose, no rationale, no ticket refs, no future work. Each section answers "what must I do?" -->

# Documentation - HTML

## When to Activate

- Creating a new requirement, migration plan, or maintenance ticket
- Writing acceptance criteria or scope descriptions
- Estimating story points
- Reviewing or updating existing docs for accuracy

## Required Metadata Fields

Every document must include bold metadata fields immediately after the `# Title` line.

```markdown
# Title

**Type:** Task
**Priority:** High
**Severity:** High
**Story Points:** 5
**Assignee:**
**Repository:** html
**JIRA Ticket:**
```

| Field | Required | Values |
|---|---|---|
| `**Type:**` | Yes | `Task`, `Story`, `Bug` |
| `**Priority:**` | Yes | `High`, `Medium`, `Low` |
| `**Severity:**` | Yes | `High`, `Medium`, `Low` |
| `**Story Points:**` | Yes | `1`, `2`, `3`, `5`, `8`, `13`, `21` |
| `**Assignee:**` | Yes | Leave blank |
| `**Repository:**` | Yes | `html` |
| `**JIRA Ticket:**` | No | Populated after ticket creation |
| `**Epic:**` | No | Parent epic key |
| `**Sprint:**` | No | Sprint name |

## Document Structure

```markdown
# Title

**Type:**
**Priority:**
**Severity:**
**Story Points:**
**Assignee:**
**Repository:**
**JIRA Ticket:**

## Scope

Brief description of what this covers.

---

## Items / Details

Detailed breakdown of work items.

---

## Acceptance Criteria

- [ ] Criterion 1
- [ ] Criterion 2
```

## Requirements Directory Placement

This repository has no `docs/` directory. Requirement documents live in the consuming application repository, not here.

Only create a document in this repository when explicitly asked. If asked, create `docs/requirements/` and place the file in the correct subdirectory:

| Directory | When to Use |
|---|---|
| `bugs/` | Fixing incorrect behavior, crashes, or production defects |
| `features/` | New capabilities, screens, or integrations |
| `maintenance/` | Refactoring, cleanup, dependency updates, config changes |
| `migration/` | Platform migration, infrastructure migration, service cutover |
| `observability-and-tooling/` | Logging improvements, dashboards, scripts, monitoring |

When ambiguous, prefer `features/` for new behavior and `maintenance/` for internal-only changes.

## File Naming

Kebab-case slug only - no ticket prefixes.

- `ios-build-config-update.md`
- `home-feed-empty-state-fix.md`

## Requirements Writing Principles

Requirements describe what and why - never how at the code level.

### Prose Style

- Plain, direct language
- One sentence per requirement when possible
- Bullet points over paragraphs
- No introductory preambles

## HTML Doc Focus

- Prefer documenting gameplay behavior, asset sources, browser compatibility, and performance constraints
- Include supported input methods (touch, mouse, keyboard) when relevant
- Document fallback behavior when remote assets fail to load

### Language Boundaries

Never reference file paths, function names, class names, line numbers, types, variable names, or import paths.

Use behavioral language instead.

Allowed specifics: API endpoint paths, environment variable names, HTTP status codes, browser/platform names, external service names.

## Acceptance Criteria Rules

- Each criterion is independently verifiable
- State observable outcomes, not implementation steps
- Gate environment promotion explicitly when relevant
- Use checkboxes: `- [ ] Criterion`

## Markdown Formatting Rules

### Tables

- Single leading pipe per row
- Every table needs header, separator, and matching data columns
- Escape `|` inside cells with `\|`

### Headings

- Space after `#`
- Blank line before every heading

### Code Fences

- Every opening fence must have a matching closing fence

### Indentation

- Spaces for nested lists, never tabs

## Story Point Estimation

| Points | Complexity | Est. Hours | Example |
|---|---|---|---|
| 1 | Trivial | 0.5-1h | Copy update, constant change |
| 2 | Simple | 1-3h | Small UI fix in one screen |
| 3 | Small | 3-6h | New hook with tests |
| 5 | Medium | 6-12h | New screen flow with API integration |
| 8 | Large | 12-24h | Multi-screen feature with platform handling |
| 13 | XL | 24-40h | Cross-cutting change with external systems |
| 21 | Epic-sized | 40h+ | Break into smaller stories |
