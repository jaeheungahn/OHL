# FAQ

## What is OHL?

OHL is a destination-aware migration toolkit for OpenClaw and Hermes.
It is designed to move agent identity, prompt, memory, and workflow material without treating migration as a blind copy.

## How should a human use OHL quickly?

Use it in this order:
- choose the route
- run the exporter
- review the migration pack
- confirm what is moved versus transformed versus excluded
- run the importer only after review

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
