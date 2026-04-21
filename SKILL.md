---
name: ohl
description: Destination-aware migration toolkit for OpenClaw and Hermes. Builds reviewable export packs, preserves original payload language, blocks silent overflow, and treats credentials as destination-side reissue material rather than migratable payload.
version: 0.1.0
author: jaeheungahn
license: CC-BY-NC-ND-4.0
---

# OHL

OHL means **OpenClaw Hermes Logistics**.

Preferred trigger names for this package:
- `OHL`
- `Soul Express`
- `OpenClaw Hermes Logistics`

Trigger guidance:
- use `OHL` as the canonical short name
- accept `Soul Express` and `OpenClaw Hermes Logistics` as explicit aliases
- do not rely on plain `logistics` as a standalone trigger because it is too broad

This skill/toolkit is for migration work between OpenClaw and Hermes where a careful, reviewable process is needed instead of a blind copy.

## One-line operating rule

Build a migration pack first, review it second, import it last.

## When to use

- when moving prompt/memory/identity material between OpenClaw and Hermes
- when you need exporter and importer roles separated
- when destination fit, overflow, or remapping risk matters
- when you need an archive/exclusion manifest in addition to import payloads

## When not to use

- when you only need a raw file copy with no transformation or safety review
- when the task is ordinary backup rather than migration
- when credentials or secret state are expected to be copied as-is

## Core rules

- never silently carry tokens, API keys, cookies, sessions, or auth blobs
- destination-side credentials are safer than credential migration
- preserve migrated payload language by default
- use explicit review gates for overflow, likely truncation, overlap, and ambiguous mapping
- prefer carry / transform / archive / exclude classification over blind file copy

## Minimal workflow

1. identify source and target
2. choose the route explicitly from the four public route cases
3. build a migration pack
4. classify into carry / transform / archive / exclude
5. review fit and overlap
6. import only after review

Recommended first interactive route question:

1. `OpenClaw -> OpenClaw`
2. `OpenClaw -> Hermes`
3. `Hermes -> Hermes`
4. `Hermes -> OpenClaw`

## Route docs

Current packaged route:
- `routes/OpenClaw-to-Hermes/export-prompt.md`
- `routes/OpenClaw-to-Hermes/import-prompt.md`
- `routes/OpenClaw-to-Hermes/mapping-rules.md`

Shared rules:
- `shared/migration-pack-schema.md`
- `shared/review-gate-rules.md`
- `shared/language-and-translation-rules.md`
- `shared/secret-and-exclusion-rules.md`
- `shared/routing-matrix.md`
- `shared/destination-path-rules.md`
- `shared/budget-decision-rules.md`

## License note

This repo currently ships as a document-and-prompt centered toolkit.

License baseline:
- `CC-BY-NC-ND-4.0`

That means people can read and use it personally with attribution, but commercial use and derivative redistribution are not allowed by default.
