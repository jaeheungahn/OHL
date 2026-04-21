# FAQ

## What is OHL?

OHL is a destination-aware migration toolkit for OpenClaw and Hermes.
It is designed to move agent identity, prompt, memory, and workflow material without treating migration as a blind copy.

한국어로 말하면:

OHL은 OpenClaw와 Hermes 사이에서 에이전트의 정체성, 프롬프트, 메모리, 운영 규칙을 옮길 때 쓰는 목적지 인식형 migration toolkit이다.
그냥 통째 복사하는 게 아니라, 무엇을 옮기고 무엇을 바꾸고 무엇을 archive/exclude 해야 하는지를 먼저 판단하는 쪽에 가깝다.

## How should a human use OHL quickly?

Use it in this order:
- choose the route
- run the exporter
- review the migration pack
- confirm what is moved versus transformed versus excluded
- run the importer only after review

한국어 빠른 사용법:
- 경로를 먼저 정한다.
- exporter로 migration pack을 만든다.
- moved / transformed / archived / excluded를 검토한다.
- 이상 없거나 승인된 뒤에만 importer를 실행한다.

## How should route selection be asked?

If OHL is asking interactively, the first route question should show all four public routes explicitly:

1. `OpenClaw -> OpenClaw`
2. `OpenClaw -> Hermes`
3. `Hermes -> Hermes`
4. `Hermes -> OpenClaw`

It should not compress those into `1 + other route` when asking the owner to choose.

한국어로는:

interactive하게 route를 고르게 할 때는 첫 질문에서 4개 경우의 수를 다 보여주는 쪽이 맞다.

1. `OpenClaw -> OpenClaw`
2. `OpenClaw -> Hermes`
3. `Hermes -> Hermes`
4. `Hermes -> OpenClaw`

즉, `1번 + 나머지는 기타 직접 입력`처럼 뭉개지 않게 해야 한다.

## How should an agent use OHL quickly?

An agent should:
- identify source and target first
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
- what is deferred or skipped
- what exact files or config surfaces are affected when that matters
- what the current move progress is

It is fine to keep a moving-house metaphor for readability, but it should still name the real technical objects, such as:
- `SOUL.md`
- `MEMORY.md`
- `agent.personalities`
- `fallback_model`

한국어로는:

초보자나 편하게 쓰고 싶은 사람에게는 번호만 던지면 안 된다.
각 선택지마다
- 고르면 다음에 뭐가 일어나는지
- 무엇이 보류되는지
- 어떤 md나 속성값이 걸리는지
- 지금 진행도가 어디쯤인지
같이 설명해주는 쪽이 맞다.
