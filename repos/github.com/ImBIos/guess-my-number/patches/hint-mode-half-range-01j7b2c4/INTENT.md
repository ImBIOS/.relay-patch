---
id: hint-mode-half-range-01j7b2c4
title: Add --hint flag to show half-range on wrong guesses
target_repo: github.com/ImBIos/guess-my-number
target_area: [index.ts]
status: applied
applied_upstream_pr: none
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

Add a `--hint` command-line flag that, when set, gives the user a half-range hint
after every wrong guess. After a wrong guess, the hint shows the range where the
secret must lie, narrowed by the guess. For example, if the range is 1-100 and
the user guesses 30 and is told "Higher", a hint would say "Hint: the secret is
in 31-100".

## Why

The game is too hard for casual play at hard difficulty. With hints, the game
becomes more accessible without removing the challenge entirely. The maintainer
might accept this but hasn't responded yet; either way, I want it in my build.

## Non-negotiables

- Flag is opt-in (`--hint`). Default behavior (just "Higher!"/"Lower!") is unchanged.
- Hint appears ON THE SAME LINE as the higher/lower feedback.
- Hint narrows the range based on the user's guess:
  - After "Higher" with guess 30 in range 1-100: hint shows `31-100`
  - After "Lower" with guess 70 in range 1-100: hint shows `1-69`
- Existing tests must still pass.
- Existing patches (e.g., `cheat-mode-reveal-01j6q3f8`) must still work.
- DO NOT modify `game.ts` — hint logic is presentation only.

## Implementation notes

- Parse `--hint` from the same `process.argv` slice (upstream v2.0.0+ already has
  `const args = process.argv.slice(2);` — piggyback on it).
- The hint message should be appended to the existing higher/lower console.log,
  OR printed as a separate line. Same-line is more readable.
- If both `--hint` and `--cheat` are passed, both work independently. The cheat
  reveals the secret at game start; the hint shows half-ranges on wrong guesses.

Previous approaches: none yet — this is the first realization.

## Implementation constraints (auto-enriched)

- DO NOT modify `game.ts` — game logic is upstream-faithful
- DO NOT add a second `process.argv.slice(2)` — upstream already has one
- MUST coexist with `cheat-mode-reveal-01j6q3f8` — do not break or duplicate the
  cheat const
