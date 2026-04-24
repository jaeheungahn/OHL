# FAQ

## What is OHL?

OHL is a destination-aware migration toolkit for OpenClaw and Hermes.
It is designed to move agent identity, prompt, memory, and workflow material without treating migration as a blind copy.

한국어로 말하면:

OHL은 OpenClaw와 Hermes 사이에서 에이전트의 정체성, 프롬프트, 메모리, 운영 규칙을 옮길 때 쓰는 목적지 인식형 migration toolkit이다.
그냥 통째 복사하는 게 아니라, 무엇을 옮기고 무엇을 바꾸고 무엇을 archive/exclude 해야 하는지를 먼저 판단하는 쪽에 가깝다.

## How should a human use OHL quickly?

Use it in this order:
- run the exporter from the source workspace
- choose what to include
- choose the destination platform or path
- review the migration pack
- run the importer only after review

한국어 빠른 사용법:
- source workspace에서 exporter를 실행한다.
- md / skills / config 중 무엇을 담을지 고른다.
- destination platform 또는 path를 정한다.
- migration pack을 검토한다.
- 이상 없거나 승인된 뒤에만 importer를 실행한다.

## How should exporter interaction be asked?

If OHL starts from a known source workspace, the exporter should detect the source platform automatically and ask what to include first:

1. `md only`
2. `md + skills`
3. `md + skills + config`
4. `additional request notes`

Then ask only for the destination platform or destination path.

The four public routes still exist internally:

1. `OpenClaw -> OpenClaw`
2. `OpenClaw -> Hermes`
3. `Hermes -> Hermes`
4. `Hermes -> OpenClaw`

But the explicit route chooser should be used mainly when the source platform is unknown or ambiguous.

한국어로는:

source workspace가 이미 분명하면, exporter는 source를 스스로 인식하고 첫 질문에서는 무엇을 담을지만 물어보는 쪽이 맞다.

1. `md만`
2. `md + skills`
3. `md + skills + config`
4. `추가 요청사항`

그 다음 destination platform/path만 짧게 묻는다. 4-route 선택지는 내부 모델로 유지하되, source가 애매할 때만 첫 질문으로 꺼낸다.

## How should an agent use OHL quickly?

An agent should:
- detect the source platform first
- ask the owner for inclusion scope, then destination
- build a migration pack instead of copying raw files
- classify items into carry / transform / archive / exclude
- stop for review if truncation, overlap, ambiguity, or destination-fit risk appears

## Why does OHL care so much about truncation?

Because migration can damage the most important parts of an agent if `SOUL`, `USER`, or memory-related payloads are silently cut.
OHL treats silent truncation as a failure mode, not as an acceptable implementation detail.

## Does OHL migrate tokens or API keys?

No, not by default.
Credentials, sessions, cookies, and raw auth material are treated as non-migratable by default.
The safer default is to re-issue or re-enter them at the destination.

## What is the most important safety idea in OHL?

Two things:
- do not silently cut important payloads like `SOUL`, `USER`, or memory
- do not carry secrets as ordinary migration content

한국어로 줄이면:
- 중요한 내용을 몰래 자르지 말 것
- 비밀정보를 평범한 이삿짐처럼 옮기지 말 것

## Does OHL preserve original language?

Yes, by default.
Migrated payloads should stay in their original language unless translation is explicitly requested for a specific payload.

## Does OHL blindly trust external contributions?

No.
Issue reports and ideas are welcome, but submitted code, prompts, and migration logic are treated as untrusted input by default.
Useful ideas may be reviewed and reimplemented rather than merged directly.

## Is OHL only for OpenClaw -> Hermes?

No.
The public route model is:
- OpenClaw -> OpenClaw
- OpenClaw -> Hermes
- Hermes -> Hermes
- Hermes -> OpenClaw

The current first package focuses on the OpenClaw -> Hermes route first.

## Where can I see ready-to-use owner prompt examples?

See `docs/owner-facing-prompts.md`.

That file contains short, copyable examples for:
- starting an OHL route
- exporter-first requests
- importer-side requests
- exporter-side config include/exclude requests
- exporter-side skill include/exclude requests
- importer-side config/skill apply-review requests
- skill recommendation and overflow review requests
- provenance disclosure requests
- export-location and handoff-path requests

한국어로는:

그 문서에 바로 복붙해서 쓸 수 있는 owner-facing 예시가 들어 있다.
예를 들면:
- OHL 경로 시작 문구
- exporter 먼저 돌리는 요청
- importer 전용 요청
- exporter에서 config review material을 pack에 넣을지 말지 묻는 문구
- exporter에서 skill artifact를 pack에 넣을지 말지 묻는 문구
- importer에서 config/skill 실제 적용 검토를 묻는 문구
- skill 추천/overflow 검토 문구
- provenance disclosure 문구
- export 위치와 handoff path 안내 문구

## How should choices be explained for beginners?

OHL should not show bare numbers with no context.

When a choice is shown, it should explain:
- what happens next if that option is chosen
- what exact files or config surfaces are affected when that matters
- what the current move progress is

It should not assume the owner already knows the internal state of OpenClaw or Hermes.
Explain the choice as if the owner may be using one or both systems for the first time.

It is fine to keep a moving-house metaphor for readability, but it should still name the real technical objects, such as:
- `SOUL.md`
- `MEMORY.md`
- `agent.personalities`
- `fallback_model`

한국어로는:

초보자나 편하게 쓰고 싶은 사람에게는 번호만 던지면 안 된다.
각 선택지마다
- 고르면 다음에 뭐가 일어나는지
- 어떤 md나 속성값이 걸리는지
- 지금 진행도가 어디쯤인지
같이 설명해주는 쪽이 맞다.

그리고 OpenClaw나 Hermes를 아직 안 써본 사람도 이해할 수 있게,
플랫폼 현재 상태를 이미 알고 있다는 전제로 말하지 않는 쪽이 맞다.
