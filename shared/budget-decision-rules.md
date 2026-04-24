# Budget Decision Rules

Every importer must decide destination fit and size fit for every payload.

## Destination states

- `direct destination`
- `absorb candidate`
- `archive candidate`
- `hold / review item`

## Size states

- `fits directly`
- `needs compression`
- `cannot safely fit`

## Rule

Silent truncation is not acceptable.
Silent destination guessing is also not acceptable.

If a payload does not clearly fit by destination, the importer must classify it as absorb / archive / hold and explain why before asking approval.
If a payload does not clearly fit by size, the importer must either prepare a reviewed compression candidate or stop for explicit review.

## Practical emphasis

- `USER` and `MEMORY` are usually the tightest targets
- `SOUL` and `AGENTS` are larger but still runtime-truncatable
- archive leftovers must be kept visible rather than silently dropped
- absorb candidates must be shown before editing durable destination files

## Skill-budget rule

Skill selection should also be treated as a destination budget problem.

- Use the latest official platform docs first.
- If the docs expose budget fields but not the current numeric default, check the live schema/runtime before finalizing recommendations.
- Keep the owner's full provisional skill selection first, even if it appears to exceed the destination budget.
- Track the current selection order and report where the owner is relative to the known budget.
- If the selected set exceeds the destination budget, do not force an early cut.
- Instead, finish collecting the preferred set, then produce a review step with overflow size and removal candidates.
- Defer detailed trim discussion until the owner finishes selecting. During selection, the workflow only needs to show running count/order and budget-relative status.
- After selection is complete, explain the overflow and recommend which skills to remove with short reasons.
- If the destination still has free capacity, use the remaining-slot count as the default recommendation size for one-pass search and one-batch activation.
- After showing the recommended list up to that remaining count, approval may activate/import that full approved batch at once.
- Recommended skill lists should include a short explanation for each item: what the skill is and why it is recommended.

Current platform-specific guidance:

- OpenClaw official docs state that the compact skills block in the system prompt is bounded by `skills.limits.maxSkillsPromptChars`, and the official config/schema surface also exposes `skills.limits.maxCandidatesPerRoot`, `maxSkillsLoadedPerSource`, `maxSkillsInPrompt`, `maxSkillsPromptChars`, and `maxSkillFileBytes`.
- In the current OpenClaw runtime defaults, those resolve to `maxCandidatesPerRoot=300`, `maxSkillsLoadedPerSource=200`, `maxSkillsInPrompt=150`, `maxSkillsPromptChars=18000`, and `maxSkillFileBytes=256000` unless overridden.
- Hermes official docs describe skills as progressive disclosure, so there is not necessarily one global installed-skill cap in normal use. However, Hermes official FAQ does document a Telegram-facing 100 slash-command limit and additional Telegram payload-size pressure.

Recommended removal candidates should prefer:

- overlapping skills
- low-priority convenience skills
- platform-mismatched skills
- dependency-heavy or runtime-unready skills
- skills that duplicate built-ins or already-approved destination skills
