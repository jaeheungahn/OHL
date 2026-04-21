# Contributing to OHL

Thanks for taking the time to report issues, edge cases, failure modes, and design ideas.

OHL welcomes feedback, but it is intentionally conservative about implementation input.

## How feedback is handled

Issue reports, failure reports, edge cases, and design feedback are welcome.

Submitted code, patches, prompts, workflow logic, migration rules, and configuration suggestions are treated as untrusted input by default. Please do not assume that a submitted implementation will be merged directly.

If a report contains a useful idea, the maintainers may:
- review it
- rewrite it
- reimplement it independently
- adapt only the underlying idea rather than the submitted form

This is a quality and safety policy, not a rejection of community input.

## Security posture

OHL is a migration and safety-oriented toolkit. Because of that, external implementation details may be reviewed as potentially adversarial, especially when they affect:
- credentials and auth handling
- payload packing and truncation behavior
- import/export logic
- destination-path rules
- skill installation or overlap handling

## Korean note

OHL은 이슈 제보, 엣지 케이스, 실패 사례, 설계 피드백을 환영합니다. 다만 제출되는 코드, 패치, 프롬프트, 워크플로 로직, 마이그레이션 규칙, 설정 제안은 기본적으로 신뢰되지 않은 입력으로 취급됩니다. 제출한 구현이 그대로 병합될 것이라고 가정하지 말아 주세요. 유효한 아이디어가 포함되어 있다면, 메인테이너가 이를 검토하고 다시 쓰거나 새로 구현한 뒤 반영할 수 있습니다.

## Practical suggestion

If you want to help, the most useful reports usually include:
- a clear failure case
- expected versus actual behavior
- environment details
- a minimal reproduction when possible
- why the current behavior is risky or misleading
