# Copilot Instructions - HTML

## Context

Static HTML game repository. Each game is a single self-contained `.html` file with inline CSS and script, loaded in a React Native WebView.

No build step, no bundler, no package manager, no module system.

## Architecture

### Directory Structure

**`*.html`** - One file per game, fully self-contained:

| File | Game | Orientation |
|---|---|---|
| `sigaboGame.html` | Sigabo Dash (endless runner) | Portrait |
| `sigaboPlatformer.html` | Sigabo platformer | Portrait |
| `sigaboRunAndGun.html` | Sigabo Breakpoint (endless run-and-gun) | Landscape |
| `babyDollsMatch.html` | Baby Dolls match-three | Portrait |
| `biniTriviaGame.html` | BINI trivia | Portrait |

**`.github/skills/`** - Skill definitions and repo-specific authoring rules

Game assets are not in this repo. They live in the sibling `images/joinnow-app/<brand>/assets/` folder.

### Asset References

| Style | Used by | Rule |
|---|---|---|
| Absolute `https://raw.githubusercontent.com/mvbrazas/images/refs/heads/main/joinnow-app/...` | `sigaboGame.html`, `sigaboPlatformer.html` | Asset must be pushed to the images repo before release |
| Relative `../images/joinnow-app/...` | `sigaboRunAndGun.html` | Requires the images folder to be served alongside `html/` |

Match the existing convention of the file being edited. Do not mix styles within one file.

### Layers

HTML -> CSS -> Canvas script -> WebView `postMessage` bridge.

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

- **Script style:** ES5 inside an IIFE. Use `var`, `function` declarations, and `.then()` chains. Do not introduce `let`, `const`, arrow functions, classes, or modules into existing files.
- **UI composition:** Keep markup minimal and readable; avoid unnecessary wrapper layers.
- **Error handling:** Catch runtime errors and show safe fallback states.
- **Image loading:** Track an `imageReady` flag set in `onload`, and keep a vector or rectangle fallback path that draws until the image resolves.
- **Validation:** Validate postMessage payloads before acting.
- **Constants:** Centralize game tuning values near the top of the script.
- **Performance:** Avoid heavy loops and expensive per-frame allocations in animation code.

## Sprite Sheet Conventions

- Pack frames into a uniform grid; store cell width, cell height, and the feet/baseline offset as named constants
- Bottom-align characters to a shared baseline so physics, not art, controls vertical position
- Anchor horizontally on the footprint, not the bounding box, so extended weapons do not shift the character
- Record the source art's facing direction; use a `flip` multiplier when art faces left
- Store measured attachment points (muzzle, door opening) as constants in cell coordinates and convert to world space at use
- Keep the unpacked original alongside the packed sheet as `<name>-source.png`

## Endless Level Conventions

- Generate content in fixed-width chunks ahead of the player; never precompute a fixed-length level
- Cull entities behind the camera every frame
- Derive scenery from a deterministic seeded function of world index so parallax layers never reshuffle while scrolling

## Secrets and Environment

- All secrets come from environment variables or secure native/app configuration.
- `.env` files and platform secret files must remain out of version control.
- Never store secrets in JS constants, screen state defaults, or sample fixtures.

## Network Standards

**Methods:** Use simple `GET` for static assets unless write behavior is explicitly required.
**Status codes:** Handle common codes explicitly and map failures to fallback visuals/UI.
**Timeouts:** Guard remote fetches with fallback behavior.
**House ads:** Fetched from the shared house-ads endpoint. A failed fetch must leave the game fully playable with no billboard drawn.

## Naming

- Files: follow existing naming in each folder; keep conventions consistent within the folder.
- Constants: reuse existing constants in the same file before adding new ones.

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
