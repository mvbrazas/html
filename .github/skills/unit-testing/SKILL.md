---
name: unit-testing
description: Verification rules for HTML games - manual browser checks, regression checklist, and what to prove before declaring work complete.
---

<!-- AUTHORING RULE: Rules and decision tables only. No narrative prose, no rationale, no ticket refs, no future work. Each section answers "what must I do?" -->

# Verification - HTML

## When to Activate

- After any gameplay, rendering, or asset change
- Before declaring work complete
- When changing physics, collision, or tuning constants

## Tooling Reality

This repository has no test runner, no package manager, and no module system. There is no `package.json`, `tsconfig.json`, or Jest config.

- Do not add `.test.ts` / `.test.js` files
- Do not add Jest, Vitest, or any test dependency without an explicit request
- Verification is manual, in a browser, against the running game

## Required Checks Before Completion

- [ ] Game loads with no console errors
- [ ] Start, game over, revive, and restart paths all reachable
- [ ] Every new sprite renders at the intended scale and baseline
- [ ] Image fallback path still draws when the asset fails to load
- [ ] Touch controls and keyboard controls both work
- [ ] Target orientation renders correctly

## Physics and Collision Changes

When changing player size, obstacle size, jump strength, gravity, or speed, prove the level is still completable.

- Compute airborne time and peak height from the jump constants
- Compute the crossing distance as `player.width + obstacle.width`
- Confirm the clearance window exceeds the crossing distance with margin
- Confirm the tallest obstacle is lower than peak jump height
- Re-verify by playing, not by inspection alone

## Temporary Test Builds

To reach late-game state quickly, copy the game to a scratch file and reduce constants there.

- Name scratch copies with a leading underscore: `_sectortest.html`
- Never commit scratch copies
- Delete the scratch file once verification is done
- Never ship a file that was only verified in modified form without saying so

## Asset Verification

- [ ] Packed sheet frame count matches the frame map in code
- [ ] Baseline offset places feet/base on the ground line
- [ ] Facing direction and flip multiplier produce correct mirroring both ways
- [ ] Attachment points (muzzle, door opening) line up with the art
- [ ] No frame is clipped at its cell boundary

## Regression Checklist

- [ ] Existing games in the repo still load after shared-pattern changes
- [ ] WebView `postMessage` events still fire: `orientation`, `gameStart`, `gameOver`, `gameEnd`, `requestRevive`, `goBack`, `viewLeaderboard`
- [ ] Score finalization fires exactly once per run
