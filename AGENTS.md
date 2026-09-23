# AGENTS.md

## Repository purpose

This repository defines a multimodal **Design Reconstruction Specification (DRS)** compiler for 2D visual design.

It is specification-first and renderer-agnostic.

## Architecture rule

Use a **thin SKILL / thick references** structure.

### SKILL.md may contain only
- purpose;
- input/mode routing;
- required reference reading order;
- high-level execution sequence;
- hard boundaries;
- completion test.

### references/ owns domain detail
Put detailed rules here:
- taxonomy;
- visual-analysis method;
- canonical fields;
- geometry;
- anchors;
- constraints;
- attention;
- style tokens;
- output shape;
- schema;
- examples.

Do not grow `SKILL.md` into a handbook.

## Invariants

1. **Analyze and specify; do not render.**
2. **Semantic decomposition beats pixel tracing.**
3. **Canonical geometry uses normalized `{x,y,w,h}` with top-left origin.**
4. **Semantic hierarchy must be preserved.**
5. **Relationships must be represented through anchors/constraints when important.**
6. **Observed, inferred, and proposed are distinct provenance classes.**
7. **Uncertainty is first-class data.**
8. **Human View and Machine View must describe the same model.**
9. **Material taxonomy is controlled.**
10. **Schema-breaking changes require versioning.**

## Canonical files

- `SKILL.md` — router/orchestrator.
- `references/reference-index.md` — reference map.
- `references/canonical-schema.md` — field semantics.
- `references/schema/design-reconstruction-spec.schema.json` — executable Machine View contract.
- `references/output-contract.md` — Human/Machine final-output contract.

## Change checklist

When changing DRS fields:
1. update the JSON Schema;
2. update `references/canonical-schema.md`;
3. update affected references;
4. update at least one Human and Machine example;
5. change `SKILL.md` only if orchestration behavior changes;
6. preserve backward compatibility or bump `spec_version`.

When changing material types:
1. update `references/material-taxonomy.md`;
2. update schema enums;
3. add/update examples.

## Out of scope

Do not add to the canonical core:
- final image generation;
- renderer-specific hacks;
- hard-coded brand styles;
- one-off poster schemas;
- prompts that bypass DRS;
- undocumented magic coordinates.

Optional downstream adapters may consume DRS later, but must not redefine it.
