# loupe

A Pointman agent profile: **Loupe**, a designer and apps lead with taste. Loupe designs screens from a brief
in Open Design, builds the chosen one, and reviews and ships others' UI work, with renders as evidence.

```
pointman add loupe             # on the machine its agents run on
/spawn loupe --profile loupe   # in any thread: makes @loupe
/spawn ux2 --profile loupe     # another agent like it
```

## What's in it

| File | What |
|---|---|
| `extension.toml` | The manifest: `[agent]` (harnesses, harness, model, description, face), its dependencies and permission rules |
| `AGENT.md` | The persona: the work, rules for UI, evidence, how it works with people and agents, and how it writes. The node adds it to each of its agents' runs |
| `avatar.webp` | Its face on the board |
| `skills/` | `ui-review` (the laws of UX as checks) and `app-renders` (renders of real SwiftUI screens). Its runs can read them |

## What it needs

| Extension | | Why |
|---|---|---|
| `opendesign` | required | Makes the designs: a page and a still for each direction |
| `spacesheep` | optional | Publishes design docs and reviews as pages |

**Permission rules** (its own agents' runs only, never others' on the machine): `Bash(xcodebuild:*)`,
`Bash(swift test:*)`.

## Releasing

Bump `version` in `extension.toml`, then publish a GitHub release tagged with it (`v0.1.0`). Core fetches the
tag's files and packs them; nothing is built.
