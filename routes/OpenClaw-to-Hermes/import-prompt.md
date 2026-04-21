# Hermes Import Prompt for OpenClaw Migration

Usage
- Use this prompt on the **target Hermes instance**.
- Assume a review-ready export pack already exists on the OpenClaw side.
- This stage consumes the **approved export pack only**. It should not re-read raw OpenClaw source files directly.

---

Import a reviewed OpenClaw export pack into Hermes safely.
Validate fit, conflicts, and warning conditions before applying anything.
If the import would overflow, degrade, or misplace content, stop and ask for review instead of auto-finishing.

Key rules:
- no raw secret or auth import
- no silent auto-trim
- explicit review for overflow, likely truncation, conflicts, or overlap
- imported skills reviewed against Hermes built-ins and destination-owned paths
- config and skill source-path metadata inside the approved pack may be used as provenance or resume hints
- those hints do not authorize direct re-reading of raw OpenClaw source files outside the approved pack
- if those hints are present, tell the owner clearly before relying on them in a later pass
- if the approved pack includes export-location metadata, use that handoff path to help the importer find the pack quickly

Baseline mapping rule:
- treat the official Hermes automatic migration destinations as the baseline mapping where they exist
- treat official Hermes archive paths and reconstruction hints as the baseline fallback for unmapped items

Personality rule:
- Hermes officially supports `/personality` overlays and custom `agent.personalities`
- if the migration pack includes a personality preset artifact, treat that as an OHL creator-recommended route design, not as proof that Hermes automatic migration already does this by default
- if a preset is present, ask whether to keep it saved only, apply it immediately, or reject it
- if tone/style content appears duplicated across the preset, `SOUL.md`, or archived identity material, show the overlap and ask before removing anything from durable files

Skill review rule:
- before importing skills, inspect the migration pack for dependency or readiness signals such as `platforms`, `prerequisites`, `required_environment_variables`, `required_credential_files`, and `related_skills`
- if those signals suggest missing runtime conditions or agent coupling, stop for review and approval before import
- ask whether the packed skill candidates should be imported now or left packed for later
- if the owner chooses later, skip skill import cleanly and continue with the rest of the migration flow
- if the approved pack includes skill source hints, use them to recognize where the reviewed skill candidates came from instead of asking the owner for source roots again
- when a known destination skill budget exists, calculate the remaining available slots after already-active or already-kept destination skills
- use that remaining-slot count to search and prepare a recommended skill list in one pass
- show a recommended list up to the remaining-slot count, and if the owner approves, activate/import that approved list in one batch
- for each recommended skill, briefly say what the skill is and why it is being recommended for this destination

Config recommendation rule:
- ask whether the packed config review material should be used now for importer-side configuration review or left for later
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

Pack-location rule:

- expect the exporter to ask whether the reviewed pack should be written to the target agent workspace or the desktop
- expect the exporter to report a final copy-pasteable path after writing the pack
- if that location metadata is present in the approved pack, use it as the default handoff hint for the importer

Skill-count rule:

- check the latest official OpenClaw and Hermes docs before deciding whether the selected skill set fits the destination operationally
- if OpenClaw docs expose the relevant config field but not the exact current default, check the live schema/runtime too
- keep the full owner-selected set first, even if it exceeds a known destination budget
- track the current selected count and current pick order
- after selection is complete, stop for review with overflow size and removal candidates rather than silently dropping skills
- while the owner is still choosing, keep the feedback minimal: running count, pick order, and budget-relative status are enough
- after selection is complete, explain the overflow and the recommended removal list with short reasons
- if there is remaining destination capacity, use that count as the default recommendation size for a one-shot activation proposal
- recommended activation candidates should include a short per-skill explanation of role and recommendation reason
