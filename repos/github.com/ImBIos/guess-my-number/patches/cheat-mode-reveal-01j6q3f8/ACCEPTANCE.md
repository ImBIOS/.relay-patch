# Acceptance Criteria — cheat-mode-reveal-01j6q3f8

## Must pass for promotion to APPLIED

1. **Default behavior unchanged**: running `bun run index.ts` (no args) produces
   identical output to upstream. No `[CHEAT]` line appears.

2. **Cheat reveals secret**: running `bun run index.ts --cheat` prints a line
   containing `[CHEAT]` and the secret number, before the game banner.

3. **Existing tests pass**: `bun test` exits 0 with all original tests green.

4. **No game.ts changes**: the patch must not modify `game.ts`. Game logic stays
   upstream-faithful.

## How to verify

```bash
# Criterion 1: default unchanged
bun run index.ts  # should NOT show [CHEAT]

# Criterion 2: cheat works
bun run index.ts --cheat  # should show [CHEAT] before banner

# Criterion 3: tests pass
bun test

# Criterion 4: game.ts untouched
git diff upstream/main -- game.ts  # should be empty
```
