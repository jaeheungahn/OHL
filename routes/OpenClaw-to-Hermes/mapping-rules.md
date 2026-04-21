# OpenClaw -> Hermes Mapping Rules

## Fact-checked baseline: current Hermes automatic migration

The following baseline is fact-checked against the official Hermes `openclaw-migration` skill, the helper script behind `hermes claw migrate`, and the Hermes README.

### Official direct destinations

- `SOUL.md` -> `~/.hermes/SOUL.md`
- `USER.md` -> `~/.hermes/memories/USER.md`
- `MEMORY.md` -> `~/.hermes/memories/MEMORY.md`
  - merged with existing entries
  - duplicate entries removed during merge
  - overflow exported separately when limits are exceeded
- `AGENTS.md` -> `<chosen-workspace>/AGENTS.md`
  - only when a Hermes workspace target is explicitly provided
- `skills/` -> `~/.hermes/skills/openclaw-imports/`

### Official archive behavior

These do not have a direct Hermes destination in the current automatic migration baseline.
They are archived for manual review under the Hermes migration output directory.

- `IDENTITY.md`
- `TOOLS.md`
- `HEARTBEAT.md`
- `BOOTSTRAP.md`

Official archive location pattern:

- `~/.hermes/migration/openclaw/<timestamp>/archive/...`

Official Hermes guide also gives reconstruction hints for these archived items:

- `IDENTITY.md` -> merge into `SOUL.md`
- `TOOLS.md` -> Hermes has built-in tool instructions, so treat this as review material rather than a required direct import
- `HEARTBEAT.md` -> use cron jobs for periodic tasks
- `BOOTSTRAP.md` -> use context files or skills

### Official cron behavior

- OpenClaw cron configuration is archived to the migration output, not silently converted into active Hermes jobs.
- Current official baseline archives cron data for manual recreation with `hermes cron`.

## OHL enhancement layer

OHL can propose a stronger review-based remapping layer on top of the official Hermes baseline.
These are OHL recommendations, not current Hermes automatic migration defaults.

- `IDENTITY.md` -> SOUL prelude or SOUL-side durable identity section
- `TOOLS.md` -> AGENTS-side operational guidance, or archive with destination suggestion
- `HEARTBEAT.md` -> cron candidates or jobs proposal
- tone/style directives -> separate personality preset artifact
- `BOOTSTRAP.md` -> archive only unless clearly remappable

### Personality preset handling

Hermes officially supports:

- built-in `/personality` overlays
- custom personalities in `~/.hermes/config.yaml` under `agent.personalities`

OHL creator recommendation:

- When OpenClaw source material contains strong tone/style/voice instructions, prefer extracting that layer into a separate personality preset instead of blindly stacking all of it into durable `SOUL.md`.
- This keeps the durable identity layer cleaner and makes temporary or optional speaking modes easier to review, switch, and de-duplicate.
- This is the OHL creator's recommended migration direction for this route, built on top of Hermes personality features.
- It is documented here as an OHL recommendation, not as the current default behavior of official Hermes automatic migration.

So if OHL extracts a tone/style payload into a personality preset, OHL should:

1. offer to create a named custom personality entry
2. offer to apply it immediately with `/personality <name>`
3. warn that `SOUL.md` remains the durable baseline unless the owner intentionally wants the preset to carry that weight

### De-duplication rule when a personality preset is created

If tone/style content is moved into a personality preset, OHL should:

- detect overlapping tone/style lines in `SOUL.md` and archived `IDENTITY.md`
- show the duplicated lines to the owner
- ask whether to remove the overlap from the durable files
- propose replacement content categories for `SOUL.md` if removal creates empty space

Suggested replacement categories:

- durable identity
- mission and values
- behavioral defaults under ambiguity
- boundaries and avoid-rules
- non-style instructions that should remain persistent

Do not rewrite those durable files automatically. Show candidate additions first and ask for approval.

### Skill import review

Before importing skills, OHL should inspect the skill metadata and flag likely dependencies or coupling such as:

- `platforms`
- `prerequisites`
- `required_environment_variables`
- `required_credential_files`
- `related_skills`

If imported skills appear to depend on other skills, environment variables, commands, or platform-specific runtime conditions, OHL should report that to the owner before import and wait for approval.

### Route-aware config recommendation

OHL should also be able to generate official-doc-based config recommendations after migration planning.

This should be an optional step, not a forced step.

Recommended flow:

1. on the exporter side, ask only whether config review material should be included in the migration pack
2. if the owner declines, skip that packing step cleanly for the current pass
3. if the owner accepts, compare relevant OpenClaw and Hermes config surfaces using official docs and pack the review material
4. on the importer side, identify clearly similar or analogous options first
5. present recommendations and ask for approval before applying any change
6. present recommendations in small batches, preferably 5 items at a time
7. allow numeric approval replies where only the mentioned numbers are applied
8. treat any unmentioned item as held by default
9. reserve `6` as a shorthand for holding the entire current batch
10. classify high-risk config changes separately from normal suggestions
11. validate every proposed config shape against the latest official docs and current schema expectations before showing or applying it
12. if Hermes is used for the recommendation workflow, use plan mode to design the checklist only, then perform actual comparison and verification in execution mode

For the OpenClaw -> Hermes route, that can include examples such as:

- `command_allowlist`
- `agent.personalities`
- `skills.external_dirs`
- `fallback_model`
- route-relevant messaging settings

This recommendation layer should stay route-aware, so later routes such as OpenClaw -> OpenClaw, Hermes -> OpenClaw, and Hermes -> Hermes can produce different config suggestions from their own official docs.

Do not silently modify config as part of this recommendation step.
Recommendation, comparison, and approval should remain separate stages.
Do not emit guessed config syntax when the latest official docs or schema checks disagree.

Important boundary:

- if a destination does not clearly fit, do not silently compress or silently drop content
- instead, show the compression or rewrite proposal first, explain why it is needed, and stop for review

## Skill-selection boundary

If skills are part of the migration pack:

- check the latest official OpenClaw and Hermes docs for destination-facing skill limits first
- if OpenClaw docs expose the relevant config path without an exact current default, check the live schema/runtime before finalizing the budget call
- keep the owner's full preferred skill list first, even when the list appears to exceed the destination budget
- track the current count and selection order while the owner is choosing
- after the owner finishes choosing, report overflow and recommend removal candidates instead of silently dropping skills or forcing an early stop

## Required transfer boundary

Source exporter produces an approved migration pack.
Target importer consumes the approved migration pack.

## Approval gates

- export asks whether active skills should be included
- import checks skill overlap against Hermes built-ins and destination-owned paths
- overflow or likely truncation stops for explicit review

## Example request shape

Example of the intended workflow style:

> "Organize the imported OpenClaw files using the Hermes migration baseline first. Use the official Hermes automatic migration destinations where they exist. For items without a direct destination, archive them under the official migration archive path and propose reviewed remaps separately. If a payload will not fit safely, do not auto-shorten it. Show a compression proposal and the reason first, then ask for confirmation."

## Source note

This route currently treats the following as the primary official source set:

- Hermes `openclaw-migration` skill
- Hermes `hermes claw migrate` helper script
- Hermes README migration section
- Hermes `migrate-from-openclaw` guide
- Hermes personality/configuration docs for `/personality`, `agent.personalities`, and related config keys

## Accuracy boundary

This route can currently state, from primary sources, that Hermes supports `/personality` overlays and custom `agent.personalities` entries.

It does not currently claim that `tone/style -> personality preset` is the official default behavior of Hermes automatic migration.
That mapping is documented here as the OHL creator's recommended direction layered on top of the official baseline unless a primary source says otherwise.
