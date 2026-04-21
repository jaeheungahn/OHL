# OpenClaw Export Prompt for Hermes Migration

Usage
- Use this prompt on the **source OpenClaw instance**.
- The goal is not a blind copy. The goal is to build a **safe, reviewable export pack** for Hermes.
- This stage does not modify the source. It only reads, classifies, deduplicates, compresses, and reports.

---

Prepare a safe, reviewable migration export from OpenClaw to Hermes.
Do not perform a blind copy.
Build a migration pack that is deduplicated, size-aware, secret-safe, and explicitly classified into carry / transform / archive / exclude buckets.

Key rules:
- never carry secrets by default
- preserve original payload language by default
- destination-aware export decisions only
- fresh destination-side credentials are safer than auth migration
- show the raw export pack for human review before any import step
- include source-path provenance hints in the migration pack for config and skill candidates when available
- treat those hints as review metadata, not as permission for the importer to re-read raw source files later
- if those hints are included, tell the owner clearly in the export report
- before writing the pack to disk, ask whether to place it in the target agent workspace or on the desktop
- after writing the pack, tell the owner the final copy-pasteable path so the importer can find it easily

Additional route rule:
- use the official Hermes automatic migration destinations as the baseline where they clearly exist
- for items without a direct Hermes destination, prefer the official Hermes archive path and reconstruction hints first

Personality rule:
- Hermes officially supports durable `SOUL.md` identity plus `/personality` overlays and custom `agent.personalities`
- if the OpenClaw source contains a strong tone/style/voice layer, OHL treats extraction into a separate personality preset as the OHL creator's recommended direction for this route
- do not describe this as the default behavior of official Hermes automatic migration
- if a personality preset is proposed, also prepare a duplication review for overlapping tone/style text in `SOUL.md` or `IDENTITY.md`
- if a preset is created, ask whether it should be saved only, applied immediately, or rejected

Skill review rule:
- before finalizing skill export candidates, inspect likely dependency and readiness metadata such as `platforms`, `prerequisites`, `required_environment_variables`, `required_credential_files`, and `related_skills`
- report those findings for review instead of treating every skill as portable by default
- ask only whether skill transfer should happen in this pass or as a separate later pass
- if the owner chooses later, skip skill transfer cleanly for the current pass and continue with the rest of the migration pack
- when skill transfer is deferred, still record the relevant skill source metadata in the migration pack so a later pass can recognize the original source roots and winner paths without re-asking

Config recommendation rule:
- ask only whether config recommendation work should happen in this migration pass or as a separate later pass
- if the owner chooses later, skip this step cleanly for the current pass
- if the owner chooses now, compare relevant OpenClaw and Hermes config options using official docs and propose similar or analogous settings where they clearly exist
- do not apply config changes as part of recommendation generation
- when config work is deferred, still record the relevant config source metadata in the migration pack so a later pass can recognize the original source file and section origin without re-asking
- examples may include `command_allowlist`, `agent.personalities`, `skills.external_dirs`, `fallback_model`, and route-relevant messaging settings

Owner-facing disclosure rule:

- if the migration pack includes config or skill source hints, say that clearly in the review output
- explain that those hints are for provenance and later resume convenience
- explain that the importer should still rely on the approved pack rather than silently re-reading raw OpenClaw source files
- if the exporter writes the pack to disk, say clearly where it was written and provide a copy-pasteable path for the importer
- when presenting recommendations, use small batches of at most 5 items
- ask for numeric approval only, where only the mentioned numbers are applied
- treat unmentioned items as held by default
- allow `6` as a shorthand meaning: hold the entire current batch
- separate high-risk config changes into their own review section
- validate any proposed Hermes config syntax against the latest official docs and schema expectations before presenting it
- if Hermes is being used to run the recommendation workflow, plan mode may be used to design the checklist, but actual comparison and verification should happen in execution mode

Skill-count rule:

- check the latest official OpenClaw and Hermes docs before deciding whether the selected skill set is safely portable
- if OpenClaw docs expose the relevant config field but not the exact current default, check the live schema/runtime too
- keep collecting the owner's preferred skills even if the set appears to exceed a known destination budget
- track the current selected count and the owner's current pick order
- after selection is complete, show overflow and recommend removal candidates instead of silently trimming or blocking early
- while the owner is still choosing, avoid expanding into detailed trim-option discussion beyond running count and budget status
- once the owner finishes choosing, explain the overflow and the recommended skills-to-remove list with short reasons
