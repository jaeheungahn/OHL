# Review Gate Rules

OHL uses explicit review gates as hard safety checks, not courtesy warnings.

## Confirmation is required for

- payload overflow
- likely runtime truncation
- file mapping ambiguity
- archive/import boundary ambiguity
- destination-path uncertainty
- skill overlap
- skill dependency or runtime-readiness uncertainty
- secret ambiguity
- noisy or risky cron/automation proposals
- duplicate personality guidance spread across SOUL, IDENTITY, and personality preset candidates
- route-aware config recommendation ambiguity

## Rule

If a risky condition is present, the workflow must stop and ask for review.
Do not auto-finish with a soft warning.

Special cases:

- If a personality preset candidate is created during export, pack it as a review artifact and defer the save/apply/reject decision to the importer stage.
- If a personality preset candidate is present during import, ask whether it should be applied immediately, kept as a saved preset only, or rejected.
- If removing duplicated tone/style text from durable files would change the long-term identity surface, ask before editing.
- If skill metadata suggests missing env vars, commands, credential files, or related skill coupling, ask before import.
- If skill handling is optional, exporter should ask only whether skill artifacts should be included in the pack, and importer should ask later whether those packed skill candidates should actually be imported.
- If config handling is optional, exporter should ask only whether config review material should be included in the pack, and importer should ask later whether to use that packed review material for actual target-side configuration review.
- If config recommendations are generated, ask before applying any recommended config change.
- If messaging or model/provider setup would require fresh secrets, present manual setup guidance and commands only. Do not complete secret entry on the owner's behalf.
- If destination bot setup could collide with another bot's `.env` or shared token file, warn explicitly and ask whether the owner wants safe preservation guidance for the existing token before any setup notes are finalized.
- When config recommendations are shown, prefer batches of at most 5 items.
- Numeric approval should be sparse by default: only the mentioned numbers move forward.
- Any item not mentioned stays on hold.
- `6` may be used as a shorthand for holding the current batch.
- High-risk config changes should be shown in a separate review section.
- Before presenting or applying config syntax, validate it against the latest official docs and current schema expectations.
- When skill selection exceeds a known destination budget, stop for review after the owner finishes selecting. Show current count, known budget basis, overflow amount, and removal candidates.
- When a recommended skill batch is sized to remaining destination capacity, show that count clearly before approval and only activate/import the full batch after explicit owner approval.
- If source-path provenance hints are included for later config or skill passes, disclose that clearly to the owner and explain their purpose.
- If the exporter is about to write the migration pack to disk, ask whether it should go to the target agent workspace or the desktop.
- After writing the pack, disclose the final copy-pasteable path clearly so the importer can find it easily.

## Output expectation

User-facing review questions should be:
- short
- explicit
- destination-aware
- written in the preferred interface language when confidence is high
- friendly enough for first-time users, not just experts

When a numbered choice is shown, it should also explain:
- what happens next if the owner chooses that option
- which exact files, payloads, or config surfaces are affected when relevant (for example `SOUL.md`, `MEMORY.md`, `agent.personalities`, `fallback_model`)
- where the owner currently is in the move, for example `route chosen -> pack built -> import review pending`

For most beginner-facing choice prompts, the useful minimum is:
- current move progress
- what happens next
- which real files or config surfaces are involved

Only add defer/skip narration when leaving it out would create real confusion.

Also assume the owner may be new to both platforms.
Do not explain choices as if the owner already knows the current state of OpenClaw or Hermes internals.

## Tone rule

Use gentle wording in review prompts, but keep the real risk explicit.
For example, it is okay to say the pack needs more careful packing for the move, but it is not okay to hide meaning-loss or overflow risk.

It is good to keep the moving-house metaphor for readability, but the metaphor should not replace exact technical names.
Good style:
- friendly move-language for the overview
- exact md filenames, config keys, and destination paths for the real decision surface

For completion messages, also prefer high visual scanability:
- short heading or first line that clearly says the step is done
- one path per line when paths matter
- avoid turning the handoff into a dense wall of instructions when a shorter next-step cue is enough
