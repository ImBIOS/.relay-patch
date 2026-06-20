# ImBIOS's .relay-patch

Patch intents for [relay-patch](https://github.com/ImBIOS/relay-patch).

## Patches

| Repo | Patch | Status | Upstream PR |
|---|---|---|---|
| [guess-my-number](https://github.com/ImBIOS/guess-my-number) | [cheat-mode-reveal](repos/github.com/ImBIOS/guess-my-number/patches/cheat-mode-reveal-01j6q3f8/INTENT.md) | applied (v2) | closed (out of scope) |
| [guess-my-number](https://github.com/ImBIOS/guess-my-number) | [hint-mode-half-range](repos/github.com/ImBIOS/guess-my-number/patches/hint-mode-half-range-01j7b2c4/INTENT.md) | applied (v2) | — |
| [natively-cluely-ai-assistant](https://github.com/Natively-AI-assistant/natively-cluely-ai-assistant) | [add-native-linux-support](repos/github.com/Natively-AI-assistant/natively-cluely-ai-assistant/patches/add-native-linux-support-with-wayland-primary-and--jx3xp10k/INTENT.md) | applied (v1) | [#327 (draft)](https://github.com/Natively-AI-assistant/natively-cluely-ai-assistant/pull/327) |

## Conventions

Each patch directory contains:

- `INTENT.md` — natural-language intent + acceptance criteria (the truth)
- `ACCEPTANCE.md` — machine-checkable criteria
- `reference.diff` — last successful realization (evidence, not source of truth)
- `verify.sh` — runnable verification script (the safety net)
- `attempts.jsonl` — history of attempts (learn from failures)

Layout:
```
repos/
  github.com/
    <owner>/
      <repo>/
        manifest.json       # patch metadata, drift tracking, sibling order
        patches/
          <patch-id>/
            INTENT.md
            ACCEPTANCE.md
            reference.diff
            verify.sh
            attempts.jsonl
```

For details on how relay-patch works, see [github.com/ImBIOS/relay-patch](https://github.com/ImBIOS/relay-patch).
