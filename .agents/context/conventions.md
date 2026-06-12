# Conventions
> Second routing layer for principles. Load this file before reaching into `principles/`.

## Source Layout
```
principles/            ← agent-only principles (manually maintained, NOT generated from /docs)
principles/distilled/  ← READ-ONLY · auto-generated from /docs on each pipeline run
```

## Freshness
Only `principles/distilled/` regenerates (driven by `/docs`). `principles/` is stable and manually maintained.
If a rule conflicts with `architecture.md` or `domain.md`, the most recently dated ADR wins — file a new ADR rather than patching either source.
 