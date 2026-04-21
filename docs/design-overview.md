# Design Overview

OHL is not a blind copier.
It is a migration toolkit that treats transfer as a reviewed packaging problem.

## Core idea

```text
Source Platform -> Source Exporter -> Migration Pack -> Target Importer -> Target Platform
```

## Why this exists

OpenClaw and Hermes do not have a one-to-one file model.
Some files map cleanly, some need transformation, and some should be archived or excluded.

## Design goals

- explicit exporter/importer separation
- destination-aware decisions
- no silent secret carry
- no silent overflow acceptance
- original-language payload preservation
- explicit review gates for risky decisions

## Important remapping rules

- Official Hermes baseline:
  - `SOUL.md` -> `~/.hermes/SOUL.md`
  - `USER.md` -> `~/.hermes/memories/USER.md`
  - `MEMORY.md` -> `~/.hermes/memories/MEMORY.md`
  - `AGENTS.md` -> chosen Hermes workspace path
  - `skills/` -> `~/.hermes/skills/openclaw-imports/`
  - `IDENTITY.md`, `TOOLS.md`, `HEARTBEAT.md`, `BOOTSTRAP.md` -> archive for manual review
- OHL enhancement layer:
  - `IDENTITY.md` -> SOUL-side durable identity content
  - `TOOLS.md` -> AGENTS-side operational guidance
  - `HEARTBEAT.md` -> cron candidates, not direct copy
  - tone/style -> separate personality preset

The tone/style -> personality preset rule is documented in OHL as the OHL creator's recommendation, not as a claim that Hermes automatic migration already does this by default.
It is recommended because Hermes already distinguishes durable identity in `SOUL.md` from temporary personality overlays.

If a reviewed remap exceeds the safe destination budget, OHL should propose compression explicitly instead of silently truncating it.

## Current first package focus

This first GitHub-ready package focuses on the OpenClaw -> Hermes route and the shared rules needed to expand later.
