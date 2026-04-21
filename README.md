# OHL OpenClaw Hermes Logistics - Soul Express OHL

Destination-aware migration toolkit for OpenClaw and Hermes.

OHL packages migration rules, route-specific prompts, and safety guidance into a repo-ready skill/toolkit format so teams can review what moves, what is transformed, what is archived, and what must never be carried.

## In one sentence

OHL helps move an agent between OpenClaw and Hermes without silently cutting its important context or carrying its secrets.

## Fast mental model

Think of OHL as a careful transfer boundary:

```text
Source platform -> export review -> migration pack -> import review -> target platform
```

It is not:
- a blind copier
- a secret exporter
- a silent compressor

It is:
- a migration pack builder
- a review-gated transfer workflow
- a safety layer for `SOUL`, `USER`, memory, and related prompt material

## Status

Alpha, GitHub-first.

## Trigger names

Preferred trigger names for this package:
- `OHL`
- `Soul Express`
- `OpenClaw Hermes Logistics`

Recommended matching behavior:
- treat `OHL` as the canonical short trigger
- treat `Soul Express` and `OpenClaw Hermes Logistics` as explicit aliases
- avoid using plain `logistics` as a standalone trigger because it is too broad

This repo is being prepared for:
- GitHub publication first
- possible later submission to ClawHub or Hermes ecosystem surfaces

## What OHL does

- supports explicit migration routes between OpenClaw and Hermes
- separates exporter and importer responsibilities
- enforces explicit review gates before risky import decisions
- preserves original payload language by default
- blocks silent truncation and silent secret carry
- treats credentials, tokens, cookies, sessions, and auth material as non-migratable by default
- recommends fresh destination-side credentials as the safer path

## What moves, what changes, what does not move

### Usually moved directly or as primary payloads
- durable `SOUL`-like material
- durable `AGENTS`-like operating rules
- durable `USER` preferences

### Usually transformed before moving
- `IDENTITY.md`-style identity facts -> `SOUL` payload
- `TOOLS.md`-style runtime guidance -> `AGENTS` payload
- `HEARTBEAT.md`-style recurring behavior -> cron/job candidates
- tone/style guidance -> separate personality preset
  - in the OpenClaw -> Hermes route, this is documented as the OHL creator's recommendation, not as a claim about the official Hermes automatic migration default

### Not moved by default
- tokens
- API keys
- cookies
- session files
- raw auth state
- unclear local noise that does not belong in the target

## Core guarantees

- explicit review required for overflow, likely truncation, overlap, and ambiguous mapping
- no silent secret copy
- no credential or auth migration by default
- original-language payload preservation by default
- destination-aware packing before import
- archive and exclusion manifests kept separate from import payloads

## Supported route model

Architecture target:
- OpenClaw -> OpenClaw
- OpenClaw -> Hermes
- Hermes -> Hermes
- Hermes -> OpenClaw

Current repo-ready prompt set in this first cut:
- OpenClaw -> Hermes export prompt
- OpenClaw -> Hermes import prompt
- shared migration rules and safety docs

## Quick start

### For humans
1. Pick the route you actually need.
2. Run the exporter on the source side.
3. Review the generated migration pack.
4. Check what is carried, transformed, archived, and excluded.
5. Run the importer on the target side only after review.

### For agents or automation
1. Identify the source platform and target platform.
2. Build a migration pack, do not do a blind copy.
3. Separate payloads into carry / transform / archive / exclude.
4. Stop for review when fit, overlap, ambiguity, or truncation risk appears.
5. Never treat credentials as normal migration payload.

## Repo structure

```text
OHL/
  README.md
  LICENSE
  NOTICE.md
  CHANGELOG.md
  SKILL.md
  shared/
  routes/
  docs/
```

## Security stance

OHL is intentionally conservative.

It assumes:
- secrets are excluded unless a narrow exception is explicitly approved
- destination fit must be checked before import
- credentials should be re-issued or re-entered at the destination
- unresolved ambiguity is a stop condition, not a soft warning

## Reading guide

If you are here for a fast read:
- read `README.md` first
- read `docs/faq.md` second
- read `routes/OpenClaw-to-Hermes/*` only when you are using that route

If you are an agent or tool runner:
- read `SKILL.md` first
- then read the route prompt files you actually need
- use the shared rules as constraints, not as optional notes

## Feedback policy

Feedback and issue reports are welcome.

Submitted code, patches, prompts, and migration logic are treated as untrusted input by default. Useful ideas may be reviewed and reimplemented by the maintainers rather than merged directly.

Korean summary:

피드백과 이슈 제보는 환영합니다. 다만 제출된 코드, 패치, 프롬프트, 마이그레이션 로직은 기본적으로 신뢰되지 않은 입력으로 취급합니다. 유효한 아이디어는 메인테이너가 직접 검토한 뒤, 그대로 병합하지 않고 재작성 또는 재구현하여 반영할 수 있습니다.

## License

Unless otherwise noted, this repository is released under:
- `CC-BY-NC-ND-4.0`
- Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International

To keep GitHub license detection as clean as possible, `LICENSE` keeps the canonical license text and repository-specific attribution is kept in `NOTICE.md`.

Practical meaning for this repo:
- personal use allowed
- attribution required
- commercial use prohibited
- redistribution of modified derivatives is not allowed under the default license

If this repo later grows a substantial executable code layer, the code license may be split from the docs/prompt license in a later revision. This first public GitHub packaging is document-and-prompt centered.

## Suggested first upload set

For the first GitHub push, the minimum sensible set is:
- `README.md`
- `LICENSE`
- `SKILL.md`
- `CHANGELOG.md`
- `NOTICE.md`
- `shared/*`
- `routes/OpenClaw-to-Hermes/*`
- `docs/design-overview.md`
- `docs/safety-model.md`
- `docs/faq.md`

## Attribution preference

Please keep the original repository name, license notice, and attribution chain intact when sharing or referencing this toolkit.
For formal attribution details, refer to `NOTICE.md`, `LICENSE`, and repository metadata.
