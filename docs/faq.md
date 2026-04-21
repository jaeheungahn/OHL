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
- config now/later requests
- skill import now/later requests
- skill recommendation and overflow review requests
- provenance disclosure requests
- export-location and handoff-path requests

한국어로는:

그 문서에 바로 복붙해서 쓸 수 있는 owner-facing 예시가 들어 있다.
예를 들면:
- OHL 경로 시작 문구
- exporter 먼저 돌리는 요청
- importer 전용 요청
- config를 지금 할지 나중에 할지 묻는 문구
- skill import를 지금 할지 나중에 할지 묻는 문구
- skill 추천/overflow 검토 문구
- provenance disclosure 문구
- export 위치와 handoff path 안내 문구
