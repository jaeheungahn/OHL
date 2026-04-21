# Owner-Facing Prompt Examples

These examples are not mandatory wording.
They are short starting points a human owner can copy, adapt, or say in plain language.

## Simple route start

```text
Use OHL for OpenClaw -> Hermes migration.
Build a reviewable export pack first.
Do not do a blind copy.
Ask at each meaningful step before applying changes.
```

## Export-first request

```text
Use OHL on the OpenClaw side.
Prepare a reviewable export pack for Hermes.
Use official Hermes baseline destinations first.
If something does not fit safely, do not auto-truncate it.
Show the compression proposal and reason first.
```

## Import-side request

```text
Use OHL on the Hermes side.
Consume only the approved migration pack.
Do not re-read raw OpenClaw source files directly.
If there is overflow, overlap, or destination ambiguity, stop and ask.
```

## Step-by-step approval style

```text
Use OHL.
Ask at each meaningful step before changing state.
You can do internal comparison and preparation first,
but ask before applying, importing, trimming, or activating anything.
```

## Config now or later

```text
Use OHL for OpenClaw -> Hermes.
When config work comes up, ask only whether to do it now or later.
If later, defer it cleanly.
```

## Skill import now or later

```text
Use OHL for OpenClaw -> Hermes.
When skill import comes up, ask only whether to do it now or later.
If later, defer it cleanly.
```

## Skill recommendation batch style

```text
Use OHL.
If there is destination skill capacity left, calculate the remaining slots first.
Then search and recommend up to that many skills in one pass.
For each recommended skill, say what it is and why you recommend it.
If I approve, activate/import that approved batch at once.
```

## Skill overflow style

```text
Use OHL.
Do not interrupt while I am still choosing skills.
Let me finish selecting first.
After that, show overflow amount, removal candidates, and short reasons.
```

## Provenance-hint disclosure style

```text
Use OHL.
If you store config or skill source-path metadata in the pack,
tell me clearly what metadata is included.
Explain that it is for provenance and later resume convenience,
not silent raw-source re-read permission.
```

## Export location style

```text
Use OHL.
Before writing the reviewed export pack, ask whether to place it in the target agent workspace or on the desktop.
After export, tell me the final copy-pasteable path so the importer can find it quickly.
```

## Short all-in-one request

```text
Use OHL for OpenClaw -> Hermes.
Export first, review second, import last.
Ask at each meaningful step.
Config and skill work should ask only now or later.
If you write the pack to disk, ask workspace or desktop, then tell me the final path.
```
