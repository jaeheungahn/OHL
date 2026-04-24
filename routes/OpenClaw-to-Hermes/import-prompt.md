# Hermes Import Prompt for OpenClaw Migration

Usage
- Use this prompt on the **target Hermes instance**.
- Assume a review-ready export pack already exists on the OpenClaw side.
- This stage consumes the **approved export pack only**. It should not re-read raw OpenClaw source files directly.

---

Import a reviewed OpenClaw export pack into Hermes safely.
Validate destination fit, conflicts, and warning conditions before applying anything.
If the import would overflow, degrade, or misplace content, stop and ask for review instead of auto-finishing.

## Importer interaction contract

Importer should behave like a destination-side migration operator, not like a generic question form.
It should inspect the approved pack first, explain the destination reasoning with sources, then proceed through staged confirmations.

Recommended importer flow:

1. **Analyze the pack first**
   - read the approved migration pack
   - identify route, scope, payload list, included md / skills / config material
   - do not ask the owner what is inside before inspecting it

2. **Explain OHL's recommended destination plan**
   - say what OHL recommends for each important file
   - distinguish the source of each recommendation:
     - official automatic migration destination
     - OHL-recommended path instead of archive
     - OHL creator-recommended path
     - archive fallback
   - classify each payload as:
     - `official direct destination`
     - `OHL recommended destination`
     - `OHL creator-recommended destination`
     - `archive fallback`
     - `hold / review item`

3. **Explain overflow and fit risk**
   - identify overflow, likely truncation, destination ambiguity, overlap, and unsafe-fit cases
   - show what is too large or risky and why
   - if compression or splitting is needed, show the proposed treatment before applying anything

4. **Confirm and discuss before md injection**
   - after the owner understands the destination plan and risk summary, ask for confirmation or discussion
   - only then inject/write md payloads into destination files
   - do not silently edit durable files just because a mapping exists

5. **Skill migration pass**
   - after md handling, ask whether the owner wants to bring skills too when skill artifacts exist or were requested
   - inspect skill bodies and metadata for duplicate or near-duplicate destination skills
   - report exact duplicate count and meaningful overlap count before import
   - check built-ins, destination-owned existing paths, dependencies, required env vars, credential files, and platform fit
   - then ask whether to import all, import selected, hold duplicates, or skip for later

6. **Config interpretation pass**
   - after skills, ask whether the owner wants to bring or interpret any config material
   - explain analogous settings and risky settings using official docs where possible
   - do not apply messaging, bot token, provider auth, model credential, or fallback/provider login setup on the owner's behalf
   - present config changes in small approval batches only after interpretation

7. **Finish with a clear completion summary**
   - say what was injected, archived, skipped, held, imported, or left for later
   - show final destination paths and remaining follow-ups

Importer should not present a generic first menu like `apply / review archive / adjust absorb / stop` before analysis.
The first useful owner-facing move is: **"I analyzed the pack; here is what OHL recommends and why."**

Korean owner-facing flow example:

```text
먼저 pack을 분석했어.

OHL 기준 추천은 이렇게 나뉘어:
- 공식 자동 migration destination
- archive 대신 OHL이 권장하는 실제 주입 경로
- OHL 제작자 추천 경로
- archive fallback
- 보류/review 항목

오버플로우/중복/위험은 여기 있어.
이 md 주입안으로 진행할지 먼저 상의하고, 컨펌되면 주입할게.
그다음 skills 중복검사와 import 여부를 따로 물어보고, 마지막에 config도 해석해줄게.
```

Do not ask separate yes/no questions for every file at the start.
Ask detailed questions only at the relevant stage or when a real review gate is triggered.

## Key rules

- no raw secret or auth import
- no silent auto-trim
- no silent destination guessing for ambiguous payloads
- explicit review for overflow, likely truncation, conflicts, overlap, or uncertain destination fit
- imported skills reviewed against Hermes built-ins and destination-owned paths
- config and skill source-path metadata inside the approved pack may be used as provenance or resume hints
- those hints do not authorize direct re-reading of raw OpenClaw source files outside the approved pack
- if those hints are present, tell the owner clearly before relying on them in a later pass
- if the approved pack includes export-location metadata, use that handoff path to help the importer find the pack quickly

## Baseline mapping rule

- treat the official Hermes automatic migration destinations as the baseline mapping where they exist
- treat official Hermes archive paths and reconstruction hints as the baseline fallback for unmapped items
- when a payload has no direct destination, explain whether it is better as archive or as an absorb candidate
- do not present `archive` as failure; present it as the safe fallback for material without a direct runtime slot

Example destination-fit language:

```text
`IDENTITY.md` has no clean direct Hermes slot in this pack.
Recommended handling: archive it for provenance, and optionally absorb stable identity facts into `SOUL.md` or a personality preset after review.
```

## Absorb candidate rule

Some OpenClaw files may not have a direct Hermes destination but still contain durable material.
Importer should identify absorb candidates before asking approval.

Common examples:

- `IDENTITY.md` -> archive by default; stable identity facts may be absorbed into `SOUL.md` or a personality preset after review
- `TOOLS.md` -> archive by default; durable operational rules may be absorbed into `AGENTS.md` or Hermes-local operations notes after review
- `HEARTBEAT.md` -> archive by default; actionable recurring behavior may become cron/job proposals after review
- `PENDING.md` -> exclude or archive only if explicitly requested; do not treat as durable baseline by default
- `SESSION-STATE.md` and `working-buffer.md` -> exclude by default unless explicitly requested, because they are operational working artifacts

Absorb candidates require a review gate before editing durable destination files.

## Personality rule

- Hermes officially supports `/personality` overlays and custom `agent.personalities`
- if the migration pack includes a personality preset artifact, treat that as an OHL creator-recommended route design, not as proof that Hermes automatic migration already does this by default
- if a preset is present, classify it in the mapping table first, then ask whether to keep it saved only, apply it immediately, or reject it
- if tone/style content appears duplicated across the preset, `SOUL.md`, or archived identity material, show the overlap and ask before removing anything from durable files

## Skill review rule

- if the pack includes skill candidates, list them as a separate `skill review` section after the main destination mapping
- before importing skills, inspect the migration pack for dependency or readiness signals such as `platforms`, `prerequisites`, `required_environment_variables`, `required_credential_files`, and `related_skills`
- if those signals suggest missing runtime conditions or agent coupling, stop for review and approval before import
- ask whether the packed skill candidates should be imported now or left packed for later only after showing the review summary
- if the owner chooses later, skip skill import cleanly and continue with the rest of the migration flow
- if the approved pack includes skill source hints, use them to recognize where the reviewed skill candidates came from instead of asking the owner for source roots again
- when a known destination skill budget exists, calculate the remaining available slots after already-active or already-kept destination skills
- use that remaining-slot count to search and prepare a recommended skill list in one pass
- show a recommended list up to the remaining-slot count, and if the owner approves, activate/import that approved list in one batch
- for each recommended skill, briefly say what the skill is and why it is being recommended for this destination

## Config recommendation rule

- if the pack includes config review material, list it as a separate `config review` section after the main destination mapping
- ask whether the packed config review material should be used now for importer-side configuration review or left for later only after showing what config surfaces are involved
- if the owner chooses later, skip this step cleanly for the current pass
- if the owner chooses now, compare relevant OpenClaw and Hermes config options using official docs and propose similar or analogous settings where they clearly exist
- present recommendations for approval before applying any config change
- if the recommendation touches messaging connections, bot tokens, provider auth, model credentials, or fallback/provider login state, do not complete that setup on the owner's behalf
- in those cases, you may provide exact command examples or config snippets, but instruct the owner to obtain fresh credentials and complete the final setup manually
- if the approved pack includes config source hints, use them to recognize which reviewed source config file or sections the recommendations came from instead of asking the owner for that source again
- examples may include `command_allowlist`, `agent.personalities`, `skills.external_dirs`, `fallback_model`, and route-relevant messaging settings
- when presenting recommendations, use small batches of at most 5 items
- ask for numeric approval only, where only the mentioned numbers are applied
- treat unmentioned items as held by default
- allow `6` as a shorthand meaning: hold the entire current batch
- separate high-risk config changes into their own review section
- validate any proposed Hermes config syntax against the latest official docs and schema expectations before presenting or applying it
- if Hermes is being used to run the recommendation workflow, plan mode may be used to design the checklist, but actual comparison and verification should happen in execution mode

## Pack-location rule

- expect the exporter to ask whether the reviewed pack should be written to the target agent workspace or the desktop
- expect the exporter to report a final copy-pasteable path after writing the pack
- if that location metadata is present in the approved pack, use it as the default handoff hint for the importer

## Skill-count rule

- check the latest official OpenClaw and Hermes docs before deciding whether the selected skill set fits the destination operationally
- if OpenClaw docs expose the relevant config field but not the exact current default, check the live schema/runtime too
- keep the full owner-selected set first, even if it exceeds a known destination budget
- track the current selected count and current pick order
- after selection is complete, stop for review with overflow size and removal candidates rather than silently dropping skills
- while the owner is still choosing, keep the feedback minimal: running count, pick order, and budget-relative status are enough
- after selection is complete, explain the overflow and the recommended removal list with short reasons
- if there is remaining destination capacity, use that count as the default recommendation size for a one-shot activation proposal
- recommended activation candidates should include a short per-skill explanation of role and recommendation reason
