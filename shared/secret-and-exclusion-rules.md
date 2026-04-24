# Secret and Exclusion Rules

## Never migrate by default

- tokens
- API keys
- cookies
- session files
- auth blobs
- raw credential stores
- secret env values
- `PENDING.md` unless explicitly approved
- `SESSION-STATE.md`
- `working-buffer.md`

## Default policy

Secrets are excluded unless a narrow exception is explicitly approved.

## Credential stance

Credentials are not normal migration payload.
The safer default is:
- re-issue at destination
- or re-enter at destination

This also applies to:
- messaging bot tokens and channel connection secrets
- model/provider API keys, OAuth state, and fallback-provider auth
- shared `.env` values or secret files that could accidentally be reused across multiple bots

If a destination setup needs those values:
- the tool may provide commands, path guidance, or config snippets
- but the owner should obtain fresh credentials and complete the final secret entry manually
- do not overwrite another bot's existing token or shared secret file casually

## Reporting

Every export/import flow should make these visible:
- what was excluded as secret material
- what was excluded as noise
- what was archived instead of imported

## Hard failure rule

If secret handling is ambiguous, stop and ask for review.
