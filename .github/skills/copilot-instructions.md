# Copilot Instructions - HTML

## Context

Static HTML game repository focused on a WebView-ready mini-game and asset files.

## Architecture

### Directory Structure

**`sigaboGame.html`** - Main standalone game page
**`assets/`** - SVG/PNG game assets (logo, player, obstacle, background)
**`.github/skills/`** - Skill definitions and repo-specific authoring rules

### Layers

HTML -> CSS -> Canvas/DOM script -> optional WebView postMessage bridge.

### Data Access

Prefer local assets. If remote assets are used, provide fallbacks for offline/failed loads.

## Simplicity Rule

**If the generated code is complex, it is wrong. Refactor until it is obvious.**

- Write code for the reader, not the machine
- One function, one responsibility - if you need to describe a function with "and", split it
- Avoid nested conditionals beyond 2 levels - extract or invert
- No premature abstractions - only abstract when the pattern repeats 3+ times
- No speculative generality - do not build for hypothetical future requirements
- If a solution requires a comment to explain what it does (not why), rewrite it
- Prefer flat over nested, explicit over clever, boring over clever

## Code Patterns

- **UI composition:** Keep markup minimal and readable; avoid unnecessary wrapper layers.
- **Error handling:** Catch runtime errors and show safe fallback states.
- **Async:** Use `async/await` for fetch and bridge flows.
- **Validation:** Validate postMessage payloads before acting.
- **Logging:** Use structured console logs with masked sensitive values.
- **Constants:** Centralize game tuning values near the top of the script.
- **Performance:** Avoid heavy loops and expensive per-frame allocations in animation code.

## Secrets and Environment

- All secrets come from environment variables or secure native/app configuration.
- `.env` files and platform secret files must remain out of version control.
- Never store secrets in JS constants, screen state defaults, or sample fixtures.

## Network Standards

**Methods:** Use simple `GET` for static assets unless write behavior is explicitly required.
**Status codes:** Handle common codes explicitly and map failures to fallback visuals/UI.
**Timeouts:** Guard remote fetches with fallback behavior.

## Naming

- Files: follow existing naming in each folder; keep conventions consistent within the folder.
- Constants: reuse existing constants in the same file before adding new ones.
- Imports: group third-party, then local modules.

## Rules

- Handle failures explicitly and return safe UI fallbacks.
- No hardcoded credentials.
- No magic strings when an existing constant exists.
- Mask sensitive data in logs (passwords, tokens, PII).
- Validate/sanitize all external payload inputs.
- Keep browser compatibility in mind for canvas and touch input APIs.
- When changing behavior, update or remove comments that describe the old behavior.
- Reuse existing utilities before creating new ones.
- Protect startup performance and runtime frame rate.

## Communication Style

- Be concise and direct - no fluff, no filler sections, no unnecessary framing.
- Do not over-structure with excessive headers, tables, or numbered lists when bullets suffice.
- Do not add sections or content beyond what is asked.
- For code suggestions, explain only what is non-obvious.
- Prefer short answers; expand only when the problem is genuinely complex.

## SKILL Authoring Rules

When adding or updating content in `.github/skills/*/SKILL.md`:

- **Rules and decision tables only** - what to do and when. No explanations of why.
- **No narrative prose** - remove phrases like "this enables..." and "the reason for...".
- **No ticket references** - skills are ticket-agnostic; history belongs in commit messages.
- **No future work notes** - unimplemented behavior does not belong in a skill.
- **No rationale bullets** - state the rule directly.
- Each section must answer: "what must I do here?" not "why does this exist?"
