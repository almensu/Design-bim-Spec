# AGENTS.md

## Repository purpose

This repository defines a multimodal **Design Reconstruction Specification (DRS)** compiler for 2D visual design.

It is specification-first, renderer-agnostic, and designed to learn from real failures without turning every correction into a permanent global rule.

## Architecture rule

Use a **thin SKILL / thick references** structure.

### SKILL.md may contain only
- purpose;
- input/mode routing;
- required reference routing;
- high-level execution sequence;
- hard boundaries;
- completion test;
- maintenance-route pointers.

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
- examples;
- gotchas;
- review gates;
- learning/evolution protocols.

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
11. **Schema validity is not the same as semantic integrity.**
12. **Normal DRS execution must not self-modify the repository.**

## Canonical files

- `SKILL.md` — router/orchestrator.
- `references/reference-index.md` — reference map.
- `references/canonical-schema.md` — field semantics.
- `references/schema/design-reconstruction-spec.schema.json` — executable Machine View structure contract.
- `references/output-contract.md` — Human/Machine final-output contract.
- `references/Gotchas.md` — repeated/high-cost failure memory.
- `references/review-checklists/drs-output-review.md` — acceptance gate.
- `references/evolution-loop.md` — lesson promotion/retirement path.
- `references/recursive-self-improvement-protocol.md` — L0/L1/L2 evidence boundary.
- `CHANGELOG.md` — English change-history source of truth.

## Before repository maintenance

1. Read `references/reference-index.md`.
2. Read task-relevant `references/Gotchas.md`.
3. Preserve high-cost failure evidence before overwriting it.
4. Identify the smallest responsibility layer that should own the fix.
5. Avoid changing `SKILL.md` if a focused reference/checklist/schema/validator is the correct landing place.

## Change checklist

When changing DRS fields:
1. update the JSON Schema;
2. update `references/canonical-schema.md`;
3. update affected references;
4. update at least one Human and Machine example;
5. change `SKILL.md` only if orchestration behavior changes;
6. preserve backward compatibility or bump `spec_version`;
7. run the DRS output review against affected examples;
8. update `CHANGELOG.md` / `CHANGELOG.zh-CN.md` for durable landed changes.

When changing material types:
1. update `references/material-taxonomy.md`;
2. update schema enums;
3. add/update examples;
4. check relevant Gotchas;
5. update changelog.

## Learning and evolution

After a meaningful maintenance task, use `references/evolution-loop.md` to decide the smallest justified landing:

```text
evidence
→ local improvement record
→ Gotcha
→ checklist
→ schema / validator / regression fixture
→ entrypoint routing
→ later-task verification
→ guarded / retired / split
```

Rules:
- one user correction does not automatically become a global rule;
- a high-cost first failure may be promoted immediately;
- a real failure used to harden a validator should be preserved as a negative fixture when practical;
- pair negative fixtures with valid positive controls;
- if a Gotcha exists but later agents never read it, routing is incomplete;
- update the changelog for actual changes, not hoped-for benefits.

## Improvement claims

Use `references/recursive-self-improvement-protocol.md`.

- L0: current issue repaired.
- L1: a durable change was used by a later task and showed benefit versus a comparable baseline.
- L2: the mechanism that generates/selects/validates improvements was itself changed, participated in the next improvement cycle, and showed benefit under stable external evaluation.

Do not claim L1/L2 because:
- docs were added;
- schema parses;
- a model self-rates higher;
- the same tuning example improved.

## Out of scope

Do not add to the canonical core:
- final image generation;
- renderer-specific hacks;
- hard-coded brand styles;
- one-off poster schemas;
- prompts that bypass DRS;
- undocumented magic coordinates;
- autonomous background self-modification.

Optional downstream adapters may consume DRS later, but must not redefine it.
