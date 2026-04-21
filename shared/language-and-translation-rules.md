# Language and Translation Rules

## Default

Migrated payload text stays in its original language.

## Translation rule

Translate a payload only when translation is explicitly requested for that specific payload.

## User-facing outputs

The following may use the preferred interface language:
- migration report
- approval questions
- summaries
- warnings

## Confidence rule

- If language confidence is high, use that language directly.
- If confidence is low, ask one clarification question and continue.

## Why this matters

OHL separates payload fidelity from interface-language convenience.
The content being moved should remain faithful to source language unless that rule is explicitly changed.
