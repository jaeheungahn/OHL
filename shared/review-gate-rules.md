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

- If a personality preset candidate is created, ask whether it should be applied immediately, kept as a saved preset only, or rejected.
- If removing duplicated tone/style text from durable files would change the long-term identity surface, ask before editing.
- If skill metadata suggests missing env vars, commands, credential files, or related skill coupling, ask before import.
- If skill import is optional, ask only whether it should happen in this pass or as a separate later pass before starting it.
- If config recommendation work is optional, ask only whether it should happen in this pass or as a separate later pass before starting it.
- If config recommendations are generated, ask before applying any recommended config change.
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

## Tone rule

Use gentle wording in review prompts, but keep the real risk explicit.
For example, it is okay to say the pack needs more careful packing for the move, but it is not okay to hide meaning-loss or overflow risk.
