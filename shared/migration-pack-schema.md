# Migration Pack Schema

A migration pack is the transfer boundary between source exporter and target importer.

## Recommended artifacts

- `SOUL_PAYLOAD.md`
- `AGENTS_PAYLOAD.md`
- `USER_PAYLOAD.md`
- `MEMORY_PAYLOAD.md`
- `PERSONALITY_PRESET.md` or `.json`  
  - recommended by the OHL creator when a strong tone/style layer should be separated from durable identity
- `CRON_CANDIDATES.md` or `.json`
- `SKILL_EXPORT_CANDIDATES.md` or `.json`
- `SOURCE_HINTS.json` or `PROVENANCE_MANIFEST.json`
  - records where config and skill candidates came from on the source side
  - examples: config file path, skill root path, winner path, workspace-relative origin, selected source section
- `EXPORT_LOCATION.md` or `.json`
  - records where the exporter wrote the reviewed migration pack
  - examples: target agent workspace path, desktop export folder, final pack directory, copy-pasteable handoff path
- `ARCHIVE_MANIFEST.md`
- `EXCLUSION_MANIFEST.md`
- `MIGRATION_REPORT.md`

## Design rule

The importer should consume the approved migration pack, not raw source files.

Source-path metadata may be included in the pack as provenance or resume hints.
Those hints help later config or skill passes recognize where candidates originally came from.
They do not authorize the importer to silently re-read raw source files outside the approved pack.

If those hints are included, the owner-facing report should say so explicitly.
It should briefly explain:

- what source-path metadata is included
- that it is there to help later config or skill passes resume cleanly
- that it does not grant silent raw-source re-read permission to the importer

If the exporter writes the pack to disk, the owner-facing report should also say:

- where the pack was written
- whether it was placed in the target agent workspace or on the desktop
- the final copy-pasteable path the importer can use to find it quickly

## Accuracy boundary

Including a `PERSONALITY_PRESET` artifact does not by itself claim that the target platform's official automatic migration already uses that structure by default.
When present in OHL, it should be understood as a route design choice or creator recommendation unless the route docs say otherwise.

## Benefit

This keeps review, deduplication, compression, and safety reporting explicit.
It also lets later config or skill passes resume without re-asking the owner where the source candidates originally came from.
