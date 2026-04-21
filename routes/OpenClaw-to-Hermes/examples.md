# OpenClaw -> Hermes Examples

## Example 1: owner-level request

```text
OpenClaw에서 가져온 파일들을 Hermes 기준으로 정리해줘.

공식 Hermes 자동 마이그레이션 destination이 있는 항목은 그 기준을 먼저 사용해.
공식 direct destination이 없는 항목은 공식 archive path 기준으로 정리하고,
필요하면 reviewed remap 후보를 따로 제안해.

payload가 destination에 안전하게 안 들어가면 자동으로 줄이지 말고,
압축안과 이유를 먼저 보여준 뒤 확인받아.

말투나 tone/style 레이어가 강하면 personality preset 분리안을 검토해.
다만 이건 Hermes 자동 마이그레이션의 공식 default라고 쓰지 말고,
OHL 제작자 권장 방향이라고 표시해.

preset을 만들면
- 저장만 할지
- 바로 적용할지
- 거절할지
물어봐.

preset으로 빠진 tone/style가 SOUL.md나 IDENTITY.md와 중복되면
중복 후보를 보여주고 제거 여부를 먼저 물어봐.
비게 되는 자리에는 어떤 durable content를 넣을지 후보도 제안해.

skills는 그냥 넣지 말고
- platforms
- prerequisites
- required_environment_variables
- required_credential_files
- related_skills
를 확인해서 종속성이나 준비 필요 사항을 보고하고 승인받아.

그리고 config 변경 추천도 자동으로 하지 말고 먼저 물어봐.
내가 원하면 그때만 OpenClaw와 Hermes 옵션을 공식 docs 기준으로 대조해서,
유사하거나 대응되는 설정이 있으면 추천안으로 보여주고 승인받아.
내가 원하지 않으면 config recommendation 단계는 스킵해.
Hermes를 쓴다면 plan mode는 비교 목록 설계에만 쓰고,
실제 대조와 점검은 execution mode에서 하게 해.
config 작업이 필요해도 이번 패스에서 할지,
아니면 migration 본체와 분리해서 나중에 따로 할지만 물어봐.
그리고 나중에 다시 할 수 있게,
output에는 config가 어디서 왔는지 경로/섹션 메타데이터를 남겨둬.
이 메타데이터를 남겼다면 사용자에게도 그 사실을 알려주고,
나중에 다시 물어보지 않기 위한 provenance hint일 뿐 원본을 몰래 다시 읽는 권한은 아니라는 점도 같이 설명해.
내보낼 때는 대상 에이전트 워크스페이스에 둘지,
바탕화면에 둘지 먼저 물어봐.
다 끝나면 importer가 바로 찾을 수 있게 복붙 가능한 최종 경로를 알려줘.
스킬도 공식 docs 기준으로 예산을 먼저 보되,
내가 고르는 중간에는 자르지 말고 지금 몇 번째 선택인지 같이 보여줘.
기준을 넘겨도 일단 끝까지 다 고르게 한 다음,
마지막에 초과분과 뺄 후보를 추천해.
skill import도 이번 패스에서 할지,
아니면 분리해서 나중에 따로 실행할지만 물어봐.
그리고 나중에 다시 할 수 있게,
어느 skill root와 winner path에서 골라진 건지도 output metadata에 남겨둬.
이것도 사용자에게 분명히 알려주고,
resume 편의를 위한 출처 힌트라는 점을 같이 설명해.
가져올 때는 남은 자리 수를 먼저 계산해서,
그 개수만큼 추천 스킬을 한 번에 검색하고 추천 목록으로 보여줘.
그 묶음을 내가 승인하면 그 batch는 한 번에 active/import 하게 해.
추천 목록에는 각 스킬이 뭔지와 왜 추천하는지도 한 줄씩 같이 붙여줘.
세부 옵션 설명은 선택이 끝난 뒤로 미루고,
그때 넘친 양이랑 왜 그 스킬들을 빼는 후보로 봤는지만 짧게 설명해.
추천은 한 번에 5개 정도씩만 보여주고,
변경할 것 번호만 말하면 그 번호만 적용 대상으로 잡아.
입력하지 않은 항목은 전부 보류로 두고,
`6`이라고 답하면 이번 배치 전체를 보류해.
위험도가 높은 변경은 일반 추천과 섞지 말고 별도 섹션으로 분리해.
그리고 config 문법은 항상 최신 공식 docs와 현재 스키마 기준으로 먼저 확인한 뒤에만 추천하거나 적용해.

끝나면
- migrated
- transformed
- archived
- excluded
- approval needed
체크리스트를 보여줘.
```

## Example 2: exporter-side request

```text
Build a reviewable OpenClaw -> Hermes migration pack.

Use official Hermes automatic migration destinations as the baseline where they exist.
For unmapped items, use the official Hermes archive path and reconstruction hints first.

Do not perform a blind copy.
Do not carry secrets by default.
Do not silently trim anything.

If a strong tone/style layer exists, you may propose a separate personality preset,
but label that as the OHL creator's recommended route design, not as the official Hermes automatic migration default.

If you create a personality preset candidate:
- ask whether it should be saved only, applied immediately, or rejected
- show overlap with SOUL.md or IDENTITY.md before removing anything
- propose durable replacement content categories if overlap is removed

Inspect skill portability before export finalization.
Report likely dependency or readiness signals from:
- platforms
- prerequisites
- required_environment_variables
- required_credential_files
- related_skills

Also include official-doc-based Hermes config suggestions when useful.

But do that only if the owner asked for config recommendation work.
If not requested, skip that step.
When showing recommendations, use batches of at most 5 items.
Ask the owner to reply with numbers only.
Any item not mentioned stays on hold.
If the owner replies `6`, hold the entire current batch.
Separate high-risk config changes from ordinary suggestions.
Validate config syntax against the latest official docs and current schema expectations before presenting or applying anything.
For skill selection, check official docs first, keep the full preferred set during selection, track the running pick order, and only recommend removals after the full set is chosen.
```

## Example 3: importer-side request

```text
Import this approved OpenClaw -> Hermes migration pack.

Use official Hermes automatic migration destinations as the baseline mapping.
Use official Hermes archive and reconstruction hints as the baseline fallback.

Stop for review if there is:
- overflow
- likely truncation
- ambiguous destination fit
- skill overlap
- skill dependency uncertainty
- personality overlap between preset and durable files

If a personality preset is included, do not assume it should become the long-term default automatically.
Ask whether it should be:
- saved only
- applied immediately
- rejected

If removing duplicated tone/style text would change durable identity files,
show the overlap first and ask before editing.

After validation, propose Hermes config recommendations if they improve fit or safety.

Only do that if the owner opted into config recommendation work.
If approved, compare OpenClaw and Hermes options using official docs and show analogous settings before applying anything.
Show at most 5 recommendations per batch.
Only the mentioned numbers should move forward.
Anything not mentioned stays on hold.
Reply `6` means hold the full current batch.
Keep high-risk config changes in a separate review section.
Check the latest official docs and schema expectations before proposing config syntax.

## Example approval format for config recommendation

```text
Config recommendation batch 1/N

1. command_allowlist
2. agent.personalities
3. fallback_model
4. skills.external_dirs
5. messaging setting alignment
6. hold all items in this batch

변경할 것 번호만 말해주세요.
입력하지 않은 항목은 보류합니다.
```
```

## Example 4: review questions OHL should ask

```text
1. This tone/style layer can be split into a separate Hermes personality preset.
   Should I save it only, apply it immediately, or reject it?

2. The following lines appear both in the preset candidate and in durable identity files.
   Do you want me to remove the overlap from the durable files, or keep both for now?

3. This skill appears to depend on missing environment variables or related skills.
   Do you want to import it now, skip it, or hold it for manual setup?

4. This payload does not safely fit the destination budget.
   Do you want to review the compression proposal before import?
```

## Durable replacement candidates after tone/style extraction

If tone/style text is removed from durable files, OHL should suggest candidates such as:

- durable identity
- mission and values
- ambiguity defaults
- boundaries and avoid-rules
- persistent non-style instructions
