# Acceptance Criteria — hint-mode-half-range-01j7b2c4

## Must pass for promotion to APPLIED

1. **Default behavior unchanged**: running `bun run index.ts` (no args) shows
   only "Higher!" / "Lower!" with no hint range. No `--hint` line appears.

2. **Hint shows on wrong guess**: running `bun run index.ts --hint` and guessing
   wrong shows a line containing both "Higher" or "Lower" AND a range like
   "31-100" or "1-69".

3. **Hint narrows correctly**:
   - Guess 30 in 1-100, told "Higher" → hint shows `31-100`
   - Guess 70 in 1-100, told "Lower" → hint shows `1-69`

4. **Existing tests pass**: `bun test` exits 0 with all original tests green.

5. **game.ts untouched**: the patch must not modify `game.ts`.

6. **Sibling patches still work**: `cheat-mode-reveal-01j6q3f8` must still
   function. Running `bun run index.ts --cheat --hint` should reveal the
   secret at start AND show hints on wrong guesses.

## How to verify

```bash
# Criterion 1: default unchanged
bun run index.ts --difficulty=hard  # no hint, no cheat

# Criterion 2 & 3: hint works
# (interactive testing required; or examine code)

# Criterion 4: tests pass
bun test

# Criterion 5: game.ts untouched
git diff upstream/main -- game.ts  # should be empty

# Criterion 6: cheat still works alongside hint
bun run index.ts --cheat --hint  # both should activate
```
