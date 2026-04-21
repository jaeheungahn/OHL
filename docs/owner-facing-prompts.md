# Owner-Facing Prompt Examples

These examples are not mandatory wording.
They are short starting points a human owner can copy, adapt, or say in plain language.

## 한국어 안내

아래 예시는 정답 문구가 아니라 출발점이다.
사람 owner가 그대로 복붙해도 되고, 말투만 바꿔서 써도 된다.

## 한국어 예시

### route 선택 첫 질문 형식

```text
OHL로 진행할 때 첫 질문은 route를 4개 경우의 수로 다 보여줘.

1. OpenClaw -> OpenClaw
2. OpenClaw -> Hermes
3. Hermes -> Hermes
4. Hermes -> OpenClaw

기타 route로 뭉개지 말고 먼저 이 4개를 번호로 보여줘.
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
Hermes 기준으로 review 가능한 export pack을 만들어줘.
공식 Hermes baseline destination을 먼저 쓰고,
안전하게 안 들어가면 자동으로 자르지 말고 압축안과 이유를 먼저 보여줘.
```

### importer 쪽 요청

```text
Hermes 쪽에서 OHL importer로 진행해줘.
approved migration pack만 사용하고,
원본 OpenClaw 파일을 다시 직접 읽지는 마.
overflow, overlap, destination ambiguity가 있으면 멈추고 물어봐.
```

### 단계별 승인 강조

```text
OHL로 진행하되, 의미 있는 단계마다 먼저 물어봐.
내부 비교나 준비는 먼저 해도 되지만,
apply, import, trim, activation 같은 상태 변경은 묻고 해줘.
```

### config 지금/나중

```text
OHL로 OpenClaw -> Hermes migration 해줘.
config 작업이 나오면 할지 말지를 길게 묻지 말고,
지금 할지 나중에 할지만 물어봐.
나중이면 깔끔하게 defer 해줘.
```

### skill import 지금/나중

```text
OHL로 OpenClaw -> Hermes migration 해줘.
skill import가 나오면 지금 할지 나중에 할지만 물어봐.
나중이면 이번 패스에서는 분리해서 넘겨줘.
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

### 짧은 통합 요청

```text
OHL로 OpenClaw -> Hermes migration 해줘.
export first, review second, import last.
의미 있는 단계마다 먼저 물어보고,
config와 skill work는 지금 할지 나중에 할지만 물어봐.
파일로 쓰면 workspace냐 desktop이냐 먼저 묻고 최종 경로도 알려줘.
```

## Simple route start

## Route-selection first question

```text
When OHL starts interactively, ask the route first with all four public cases.

1. OpenClaw -> OpenClaw
2. OpenClaw -> Hermes
3. Hermes -> Hermes
4. Hermes -> OpenClaw

Do not collapse them into an `other route` bucket at the first question.
```

## Simple route start

```text
Use OHL for OpenClaw -> Hermes migration.
Build a reviewable export pack first.
Do not do a blind copy.
Ask at each meaningful step before applying changes.
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

## Step-by-step approval style

```text
Use OHL.
Ask at each meaningful step before changing state.
You can do internal comparison and preparation first,
but ask before applying, importing, trimming, or activating anything.
```

## Config now or later

```text
Use OHL for OpenClaw -> Hermes.
When config work comes up, ask only whether to do it now or later.
If later, defer it cleanly.
```

## Skill import now or later

```text
Use OHL for OpenClaw -> Hermes.
When skill import comes up, ask only whether to do it now or later.
If later, defer it cleanly.
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

## Short all-in-one request

```text
Use OHL for OpenClaw -> Hermes.
Export first, review second, import last.
Ask at each meaningful step.
Config and skill work should ask only now or later.
If you write the pack to disk, ask workspace or desktop, then tell me the final path.
```
