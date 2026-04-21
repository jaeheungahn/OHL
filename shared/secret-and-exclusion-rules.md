# Secret and Exclusion Rules

## Never migrate by default

- tokens
- API keys
- cookies
- session files
- auth blobs
- raw credential stores
- secret env values

## Default policy

Secrets are excluded unless a narrow exception is explicitly approved.

## Credential stance

Credentials are not normal migration payload.
The safer default is:
- re-issue at destination
- or re-enter at destination

## Reporting

Every export/import flow should make these visible:
- what was excluded as secret material
- what was excluded as noise
- what was archived instead of imported

## Hard failure rule

If secret handling is ambiguous, stop and ask for review.
