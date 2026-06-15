---
id: cheat-mode-reveal-01j6q3f8
title: Add --cheat flag to reveal the secret number
target_repo: github.com/ImBIos/guess-my-number
target_area: [index.ts]
status: applied
applied_upstream_pr: closed("Cool idea but defeats the purpose of the game. Not in scope.")
version: 1
license: MIT
author: ImBIos
last_modified_by: ImBIos
owners: [ImBIos]
source_url: null
imported_at: null
created: 2026-06-14
last_realized_against_commit: cccad13
verifies_with: bun test
---

## Intent

Add a `--cheat` command-line flag that, when passed, reveals the secret number
at the start of the game. This is for testing, debugging, and casual fun.

## Why

The game is fun, but when testing changes to game logic, I need to know the
secret number immediately to verify behavior. The maintainer considers this
"defeats the purpose of the game" and won't merge it. Fair, but I want it in my
build.

## Non-negotiables

- Flag is opt-in (`--cheat`). Default behavior is unchanged.
- Secret prints BEFORE the "Guess My Number!" banner.
- Existing tests must still pass.

## Implementation notes

- Parse `process.argv.slice(2)` for `--cheat` flag at the top of `index.ts`.
- After `generateSecret()`, if `CHEAT` is true, print the secret with a `[CHEAT]`
  prefix so it's visually distinct from game output.
- No changes needed to `game.ts` — the secret generation stays the same.

Previous approach (reference.diff): 5-line addition to `index.ts`, all at the
top of the file before the game banner. Clean insertion point.
