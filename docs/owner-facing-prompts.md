# Owner-Facing Prompt Examples

These examples are not mandatory wording.
They are short starting points a human owner can copy, adapt, or say in plain language.

## 한국어 안내

아래 예시는 정답 문구가 아니라 출발점이다.
사람 owner가 그대로 복붙해도 되고, 말투만 바꿔서 써도 된다.

## 한국어 예시

### 선택지 설명 형식

```text
OHL에서 번호 선택지를 보여줄 때는 번호만 던지지 말고,
각 선택지를 고르면 다음에 뭐가 일어나는지,
그리고 지금 이사 진행도가 어디쯤인지 같이 설명해줘.

이삿짐 비유는 써도 되지만,
`SOUL.md`, `MEMORY.md`, `agent.personalities`, `fallback_model` 같은
정확한 md 이름이나 속성값도 같이 적어줘.

그리고 OpenClaw나 Hermes를 처음 쓰는 사람도 이해할 수 있게,
플랫폼 내부 상태를 이미 알고 있다는 전제로 설명하지 마.
```

### 선택지 설명 예시

```text
지금은 `OpenClaw -> Hermes` 이사에서
`export pack 생성 완료 -> importer review 대기` 단계야.

이번에 `config review material`을 pack에 넣을까?

1. 넣기
   - 다음: exporter가 `agent.personalities`, `fallback_model`, messaging 관련 review note를 pack에 넣어.

2. 넣지 않기
   - 다음: 이번 pack에서는 config review note 없이 넘어가.
```

### exporter 첫 질문 형식

```text
OHL exporter는 source 플랫폼을 스스로 인식하고,
첫 질문에서는 route 4개를 먼저 늘어놓지 말고
무엇을 담을지만 먼저 4개 보기로 보여줘.

1. md만
2. md + skills
3. md + skills + config
4. 추가 요청사항

여기서 받은 범위와 요청사항을 바탕으로,
다음 질문에서는 destination platform/path만 짧게 물어봐.
```

### 간단한 시작 문구

```text
OHL로 OpenClaw -> Hermes migration 해줘.
blind copy 하지 말고, review 가능한 export pack부터 만들어줘.
의미 있는 단계마다 먼저 물어보고 진행해.
```

### exporter 먼저 돌리는 요청

```text
OpenClaw 쪽에서 OHL exporter부터 실행해줘.
유저 질문은 2단계로만 끝내줘.

Step 1:
1. md만
2. md + skills
3. md + skills + config
4. 추가 요청사항

Step 2:
source는 네가 스스로 인식하고,
destination platform/path만 짧게 물어봐.

나머지 review 질문, 주의점, importer 판단 포인트는
팩 안의 메모나 importer 참고 프롬프트로 남겨줘.
유저를 source 쪽에서 오래 붙잡지 마.
```

### importer 쪽 요청

```text
Hermes 쪽에서 OHL importer로 진행해줘.
approved migration pack만 사용하고,
원본 OpenClaw 파일을 다시 직접 읽지는 마.

먼저 파일을 분석하고 설명해줘.
그 다음 OHL 기준 추천을 출처별로 나눠서 보여줘:
- 공식 자동 migration destination
- archive 대신 OHL이 권장하는 실제 주입 경로
- OHL 제작자 추천 경로
- archive fallback
- 보류/review 항목

오버플로우, 중복, destination ambiguity가 있으면 무엇이 왜 문제인지 먼저 설명해줘.
그 뒤 md 주입안은 컨펌/상의 후 진행해줘.
md가 끝난 다음 skills를 가져올지 물어보고,
스킬 본문까지 중복 검사해서 완전 중복/의미상 중복 개수를 보고해줘.
그 다음 config도 가져오고 싶은지 묻고, 가져온다면 네가 해석해서 추천해줘.
메세징이나 모델/provider 인증이 필요하면 명령어 예시까지만 주고,
새 credential은 내가 직접 발급받아 직접 넣게 해줘.
```

### importer 승인 스타일

```text
OHL importer는 파일마다 길게 yes/no로 묻지 말고,
먼저 pack을 분석한 뒤 OHL 추천 경로와 그 출처를 설명해줘.

흐름은 md 분석/주입 컨펌 -> skill 중복검사/import 여부 -> config 해석/적용 여부 -> 완료 요약 순서로 진행해줘.
apply, import, trim, activation 같은 상태 변경 직전에는 짧게 승인 받아줘.
```

### config 지금/나중

```text
OHL로 OpenClaw -> Hermes migration 해줘.
exporter에서는 config review material을 pack에 넣을지 말지만 물어봐.
실제 설정 검토/적용 여부는 importer에서 다시 물어봐.
```

### skill import 지금/나중

```text
OHL로 OpenClaw -> Hermes migration 해줘.
exporter에서는 skill artifact를 pack에 넣을지 말지만 물어봐.
실제 import 여부는 importer에서 다시 물어봐.
나중이면 pack 안에 provenance와 review metadata만 남겨줘.
```

### personality preset 처리

```text
OHL로 진행해줘.
exporter에서 personality preset 후보가 보이면 pack에 넣어줘.
saved/apply/reject 판단은 importer에서 물어봐.
```

### skill 추천 batch 스타일

```text
OHL로 진행해줘.
destination에 남은 skill capacity가 있으면 먼저 남은 자리를 계산해.
그 개수만큼 한 번에 검색하고 추천 목록을 보여줘.
각 스킬마다 뭔지와 왜 추천하는지도 같이 적어줘.
내가 승인하면 그 batch는 한 번에 active/import 해줘.
```

### skill overflow 스타일

```text
OHL로 진행해줘.
내가 스킬 고르는 중간에는 끊지 말고 끝까지 고르게 해줘.
다 고른 다음에 overflow 양, 뺄 후보, 짧은 이유만 보여줘.
```

### provenance hint 설명 문구

```text
OHL로 진행해줘.
config나 skill source-path metadata를 pack에 넣으면,
무슨 메타데이터를 넣었는지 나한테도 알려줘.
그리고 그게 resume 편의를 위한 provenance hint일 뿐,
원본을 몰래 다시 읽는 권한은 아니라는 점도 설명해줘.
```

### export 위치 문구

```text
OHL로 진행해줘.
export pack을 파일로 쓸 때는 대상 에이전트 workspace에 둘지,
바탕화면에 둘지 먼저 물어봐.
끝나면 importer가 찾기 쉽게 복붙 가능한 최종 경로를 알려줘.
```

### export 완료 후 안내 형식

```text
export가 끝나면 길고 복잡한 importer 프롬프트를 바로 던지지 말고,
먼저 끝났다고 분명히 알려줘.

그리고 이 3가지만 짧고 잘 보이게 알려줘:
- pack 경로
- OHL GitHub 위치
- 다음에 대상 쪽에서 실제로 말하면 되는 문장
```

### export 완료 후 짧은 안내 예시

```text
이사짐 포장 끝났어.

pack 경로:
`/path/to/pack`

OHL GitHub:
`https://github.com/jaeheungahn/OHL`

다음엔 대상 쪽에서 이렇게 말하면 돼:
- `OHL 설치`
- `Pack 임포트해줘`
- `계획대로 실행해줘`
```

### 짧은 통합 요청

```text
OHL로 OpenClaw -> Hermes migration 해줘.
export first, review second, import last.
의미 있는 단계마다 먼저 물어보고,
config와 skill work는 지금 할지 나중에 할지만 물어봐.
파일로 쓰면 workspace냐 desktop이냐 먼저 묻고 최종 경로도 알려줘.
```

## Simple route start

## Exporter first question

```text
When OHL exporter starts interactively, detect the current source platform automatically.
Do not ask the owner to choose among all four route cases first.

Ask this first instead:
1. md only
2. md + skills
3. md + skills + config
4. additional request notes

Then ask only for the destination platform or destination path.
Leave deeper review questions inside the pack for the importer stage whenever possible.
```

## Choice-explanation style

```text
When OHL shows numbered choices, explain what each option does next, what stays deferred, and where the owner currently is in the move.

It is okay to use moving-house language for readability,
but include exact technical names too, such as `SOUL.md`, `MEMORY.md`, `agent.personalities`, or `fallback_model`.
```

## Simple route start

```text
Use OHL for OpenClaw -> Hermes migration.
Build a reviewable export pack first.
Do not do a blind copy.
Keep exporter interaction short: ask what to include, then ask where to send it.
```

## Export-first request

```text
Use OHL on the OpenClaw side.
Prepare a reviewable export pack for Hermes.
Use official Hermes baseline destinations first.
If something does not fit safely, do not auto-truncate it.
Show the compression proposal and reason first.
```

## Import-side request

```text
Use OHL on the Hermes side.
Consume only the approved migration pack.
Do not re-read raw OpenClaw source files directly.
If there is overflow, overlap, or destination ambiguity, stop and ask.
```

## Exporter interaction style

```text
Use OHL.
On the exporter side, keep the owner interaction short.
Prefer a 2-step flow:
- what to include
- where to send it

Do internal comparison and preparation quietly.
Move most detailed review questions into pack notes or importer-facing prompts instead of expanding the exporter interview.
```

## Config now or later

```text
Use OHL for OpenClaw -> Hermes.
On the exporter side, include config review material only if I choose `md + skills + config` or explicitly ask for config notes.
At the importer stage, first show which config surfaces are involved, then ask whether to use or apply that config review now or later.
```

## Skill import now or later

```text
Use OHL for OpenClaw -> Hermes.
On the exporter side, include skill artifacts only if I choose `md + skills`, `md + skills + config`, or explicitly ask for skill notes.
At the importer stage, first show the skill review summary, then ask whether to actually import them now or leave them packed for later.
```

## Personality preset handling

```text
Use OHL.
If a personality preset candidate is found during export, include it in the pack as a review artifact.
At the importer stage, first classify the preset in the destination mapping, then ask whether to save/apply/reject it.
```

## Skill recommendation batch style

```text
Use OHL.
If there is destination skill capacity left, calculate the remaining slots first.
Then search and recommend up to that many skills in one pass.
For each recommended skill, say what it is and why you recommend it.
If I approve, activate/import that approved batch at once.
```

## Skill overflow style

```text
Use OHL.
Do not interrupt while I am still choosing skills.
Let me finish selecting first.
After that, show overflow amount, removal candidates, and short reasons.
```

## Provenance-hint disclosure style

```text
Use OHL.
If you store config or skill source-path metadata in the pack,
tell me clearly what metadata is included.
Explain that it is for provenance and later resume convenience,
not silent raw-source re-read permission.
```

## Export location style

```text
Use OHL.
Before writing the reviewed export pack, ask whether to place it in the target agent workspace or on the desktop.
After export, tell me the final copy-pasteable path so the importer can find it quickly.
```

## Post-export handoff style

```text
After export, do not immediately dump a long importer prompt if a shorter handoff is enough.

First say clearly that the export is done.
Then show only:
- the final pack path
- the OHL GitHub location
- explicit ready-to-say target-side lines, for example:
  - `OHL 설치`
  - `Pack 임포트해줘`
  - `계획대로 실행해줘`
```

## Short all-in-one request

```text
Use OHL for OpenClaw -> Hermes.
Export first, review second, import last.
On the exporter side, ask only two short things: what to include, then where to send it.
Move detailed review questions into pack notes or importer-facing prompts.
If you write the pack to disk, ask workspace or desktop, then tell me the final path.
```
