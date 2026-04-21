# Routing Matrix

## Public route model

- OpenClaw -> OpenClaw
- OpenClaw -> Hermes
- Hermes -> Hermes
- Hermes -> OpenClaw

## First route-selection question

When OHL starts interactively, the first route question should expose all four public routes explicitly.

Recommended numbered form:

1. `OpenClaw -> OpenClaw`
2. `OpenClaw -> Hermes`
3. `Hermes -> Hermes`
4. `Hermes -> OpenClaw`

Do not collapse routes `1, 2, 3, 4` into a vague `other route` bucket when the workflow is asking the owner to choose a route.

## Shared rules across all routes

- use a migration pack between source and target
- separate exporter and importer responsibilities
- preserve original payload language by default
- exclude secrets by default
- require explicit review for risky cases
- do not silently accept overflow or likely truncation
- support route-aware config recommendations based on official docs for the source and target platforms
- keep config recommendation work opt-in and approval-based
- keep skill import work opt-in and separable from the main migration pass

## Future capability direction

Across all four routes, OHL should eventually support:

- official-doc-based destination mapping
- official-doc-based archive and reconstruction hints
- personality/preset review where the target platform supports overlays
- skill dependency and runtime-readiness review before import
- route-specific config recommendations after migration planning

For config recommendation work across routes:

- ask only whether config work should happen now or as a separate later pass
- if later, skip cleanly for the current pass
- if now, compare source and target config options using official docs
- recommend clearly analogous settings first
- ask for approval before applying any config change
- present recommendations in batches of at most 5 items
- apply only the numbers the owner explicitly mentions
- treat all unmentioned items as held by default
- allow `6` as a shorthand for holding the entire current batch
- separate high-risk config changes from ordinary recommendations
- validate proposed config syntax against the latest official docs and current schema expectations before presenting or applying it
- when a platform supports planning-only modes, use them for checklist design only, not for the actual comparison or verification work

For skill import work across routes:

- ask only whether skill import should happen now or as a separate later pass
- if later, skip cleanly for the current pass
- keep skill import approval separate from the main content migration approval

## Personality migration guardrail

Across routes, OHL should not silently assume that an active personality preset is permanent identity.

It should ask the owner whether the active preset is:

- a temporary mode
- a durable default identity layer
- or something that should be archived but not promoted

Example implication:

- OpenClaw -> Hermes: a strong tone/style layer may be extracted into a Hermes personality preset when that fits the route design
- Hermes -> OpenClaw: if an active Hermes personality preset should become durable behavior, OHL should ask before promoting it into OpenClaw `SOUL.md` or other persistent prompt layers

Do not silently promote temporary style overlays into long-term identity files.

## Current packaged route status

- OpenClaw -> Hermes: documented in this first package
- OpenClaw -> OpenClaw: architecture defined, repo docs to expand
- Hermes -> Hermes: architecture defined, repo docs to expand
- Hermes -> OpenClaw: architecture defined, repo docs to expand
