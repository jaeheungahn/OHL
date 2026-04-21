# OpenClaw -> Hermes

This route is the first packaged route in OHL.

Included here:
- export prompt
- import prompt
- mapping rules
- examples

Operational handoff preference for this route:

- when the exporter writes a reviewed migration pack to disk, ask whether to place it in the target agent workspace or on the desktop
- after export, report the final copy-pasteable path so the importer can find the pack quickly
- after export, prefer a short visible completion message over a dense handoff block
- default handoff contents should be: `done`, final pack path, OHL GitHub location, and explicit next-step lines the owner can use on the target side
- preferred target-side wording should be concrete, for example:
  - `OHL 설치`
  - `Pack 임포트해줘`
  - `계획대로 실행해줘`

## Choice prompt style

For this route, numbered owner choices should not appear as bare options with no guidance.

Each choice prompt should say:
- where the owner currently is in the move
- what happens next for each option
- which exact files or config surfaces are affected when that matters

Default assumption:
- the owner may be new to OpenClaw, Hermes, or both
- avoid explaining the option as if the current platform state is already familiar
- use the real file or config names, then explain in plain language what they mean in this step

Example tone:
- use moving-house language to make the step easier to understand
- but still name the real technical surfaces such as `SOUL.md`, `MEMORY.md`, `agent.personalities`, `fallback_model`, or the target Hermes workspace path

Use this route when the source is OpenClaw and the target is Hermes.

## Reading order

1. `mapping-rules.md`
2. `examples.md`
3. `export-prompt.md`
4. `import-prompt.md`

## Important boundary

This route distinguishes two layers on purpose:

- the current official Hermes automatic migration baseline
- the stronger OHL review-based remapping layer

That distinction matters because some ideas that are useful in practice are not the same thing as the current Hermes automatic migration default.

Examples:

- `SOUL.md`, `USER.md`, `MEMORY.md`, `AGENTS.md`, and `skills/` have official migration destinations
- `IDENTITY.md`, `TOOLS.md`, `HEARTBEAT.md`, and `BOOTSTRAP.md` are officially archived for manual review in the current baseline
- cron is officially archived for later recreation, not silently auto-installed as active jobs

## Enhanced review ideas supported by Hermes docs

On top of the official baseline, this route can also propose:

- custom personality entries under `agent.personalities`
- optional immediate `/personality <name>` activation after preset creation
- de-duplication review between tone/style preset material and durable `SOUL.md` content
- skill dependency review before import
- optional route-aware Hermes config suggestions after migration planning

## Optional skill import step

Skill import work should also be opt-in and separable.

Recommended behavior:

- on the exporter side, ask only whether skill artifacts should be included in the migration pack
- leave actual target-side skill import questions to the importer side
- keep skill selection, overlap review, dependency review, and actual import as a distinct approval phase from the main content migration
- when a known destination skill budget exists, calculate the remaining available slots after already-kept or already-active destination skills
- use that remaining-slot count as the default recommendation batch size for skill search/review
- show a recommended skill list up to the remaining-slot count, then if the owner approves, activate/import that approved list in one batch
- when showing a recommended skill list, include a short note for each item explaining what it does and why it is being recommended

## Optional config recommendation step

Config recommendation work should be opt-in.

Recommended behavior:

- on the exporter side, ask only whether config review material should be included in the migration pack
- leave actual target-side configuration review and application questions to the importer side
- if the owner chooses now, compare OpenClaw and Hermes options using official docs
- suggest clearly similar or analogous settings first
- ask for approval before applying any config change

Execution note:

- in Hermes, plan mode is useful for designing the comparison/checklist, but it does not execute the work
- bulk comparison and verification should happen in normal execution mode, optionally using Hermes iteration budget and `--max-turns` where appropriate

Recommended approval UX:

- show at most 5 config recommendations per batch
- ask the owner to reply with numbers only for the changes they want applied
- any item not mentioned stays on hold by default
- reserve `6` as a shorthand meaning: hold all items in the current batch
- separate high-risk config changes from normal low-risk suggestions instead of mixing them into the same batch
- validate proposed config syntax against the latest official docs and schema expectations before presenting or applying changes

## Skill selection budget

For skill migration and import review, do not treat the first detected limit as a hard stop on owner choice.

Recommended behavior:

- check the latest official OpenClaw and Hermes docs first
- for OpenClaw destinations, also check the live schema/runtime when the docs expose the budget field but not the exact current default
- track the current selected skill count and the current selection order
- if the owner picks past a known destination budget, keep collecting the preferred set first
- after selection is complete, show the overflow status and suggest removal candidates instead of silently dropping or blocking items early
- while the owner is still choosing, defer other detailed option breakdowns and removal explanations until the selection pass is finished
- after the selection pass is finished, explain the overflow and the recommended removal list with brief reasons
- when the destination has remaining capacity, recommend up to that remaining count in one pass so the owner can approve a full activation batch at once
- recommended activation candidates should include short per-skill explanation lines, not just names

Route note:

- OpenClaw official docs confirm that the compact skills block is bounded by `skills.limits.maxSkillsPromptChars`, and the official config surface also includes `skills.limits.maxCandidatesPerRoot`, `maxSkillsLoadedPerSource`, `maxSkillsInPrompt`, `maxSkillsPromptChars`, and `maxSkillFileBytes`
- current OpenClaw runtime defaults are `300 / 200 / 150 / 18000 / 256000` for those five fields unless overridden
- Hermes official docs describe skills as progressive disclosure, but Hermes official FAQ also documents a Telegram-facing 100 slash-command limit and payload-size pressure

## OHL creator recommendation

For this route, OHL treats tone/style extraction into a personality preset as the OHL creator's recommended design direction.

Exporter-side rule:
- if a personality preset candidate is created, include it in the migration pack as a review artifact
- do not force the owner to choose save/apply/reject during export
- ask that question on the importer side instead

Reasoning:

- Hermes already separates durable baseline identity (`SOUL.md`) from temporary overlays (`/personality`)
- that makes tone/style review easier
- that reduces accidental duplication between durable identity files and optional speaking-mode material
- that gives the owner a cleaner approval point before applying a speaking style immediately

This is intentionally documented as the OHL creator's recommendation, not as a claim about the current default behavior of official Hermes automatic migration.

## Representative request

> "Use the official Hermes automatic migration destinations first. Archive items with no direct destination under the official migration archive path. If an item does not fit safely, do not auto-truncate it. Show the compression proposal and the reason first, then ask for confirmation."
