# Safety Model

## OHL assumes migration can fail in subtle ways

Typical failure modes:
- copying secrets by accident
- forcing mismatched files into the wrong destination
- hiding overflow behind truncation
- carrying identity/tone/ops rules without structure
- importing overlapping skills without review

## OHL response

- classify into carry / transform / archive / exclude
- keep a migration pack boundary
- require explicit review for risky cases
- keep destination-side credentials as the safer default

## Security baseline

Tokens, API keys, cookies, sessions, and raw auth material should not be transported as ordinary migration content.
They should be re-issued or re-entered at the destination.
