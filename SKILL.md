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

Exporter should stay short and low-friction.
It should normally finish in two interactive steps before pack creation.

1. detect the current source platform automatically
2. ask what to include:
   - `1. md만`
   - `2. md + skills`
   - `3. md + skills + config`
   - `4. 추가 요청사항`
3. ask only for the destination platform or destination path as needed
4. build a migration pack
5. leave most review questions, fit concerns, and import decisions inside the pack as importer-facing notes

Exporter rule:
- do not keep the owner in a long review interview on the source side
- keep exporter questions minimal
- pack later questions as importer guidance when possible
- user convenience wins over exporter-side over-questioning

Importer rule:
- analyze the approved pack before asking import questions
- explain OHL's recommended destination plan with source labels: official automatic destination, OHL-recommended path, OHL creator-recommended path, archive fallback, or hold / review item
- explain overflow, truncation, duplicate, and fit risks before applying anything
- confirm and discuss the md injection plan before writing destination files
- after md handling, run skill migration as a separate pass with body-level duplicate/overlap checking
- after skills, offer config interpretation as a separate pass
- finish with a clear summary of injected, archived, imported, skipped, and held items

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
