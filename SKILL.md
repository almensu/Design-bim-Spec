# SKILL — Design BIM Spec

## Purpose

Compile a 2D design reference or design brief into a canonical **Design Reconstruction Specification (DRS)** for downstream models.

This skill is a **multimodal visual specification compiler**, not a renderer.

```text
SEE → UNDERSTAND → CLASSIFY → DECOMPOSE → PARAMETERIZE → SPECIFY → STOP
```

## Inputs

Use this skill when the task provides either:
- a reference design image to reconstruct structurally; or
- a design brief that needs a parameterized layout specification.

## Outputs

Always produce two synchronized views:
1. **Human View** — readable reconstruction guidance.
2. **Machine View** — canonical DRS JSON.

The output contract is defined in:
- `references/output-contract.md`

## Operating modes

Choose exactly one:

- `reference_reconstruction` — a reference image exists; observe first, infer only when necessary.
- `design_planning` — no complete reference layout exists; geometry and layout are proposed.

Never conflate:
- `observed`
- `inferred`
- `proposed`

## Required reference reading order

Before execution, read:

1. `references/material-taxonomy.md`
   - classify the target material.

2. `references/visual-analysis-protocol.md`
   - perform multimodal inspection and semantic decomposition.

3. `references/canonical-schema.md`
   - understand DRS field semantics.

Then read as needed:

4. `references/layout-constraints.md`
   - bbox, anchors, constraints, layer depth, occlusion, safe area.

5. `references/attention-model.md`
   - visual fixation order and attention transitions.

6. `references/style-tokens.md`
   - measurable visual style extraction.

7. `references/output-contract.md`
   - final Human View + Machine View structure.

Machine View should conform to:
- `references/schema/design-reconstruction-spec.schema.json`

Examples live under:
- `references/examples/`

## Core execution sequence

1. Identify the canonical material type.
2. Establish canvas, aspect ratio, coordinate system, and safe area.
3. Detect semantic visual objects.
4. Build semantic groups and scene hierarchy.
5. Recover normalized geometry.
6. Recover layer depth, crop, overlap, and occlusion.
7. Recover anchors and constraints.
8. Recover visual attention order and transitions.
9. Extract measurable style tokens.
10. Mark provenance, confidence, and review needs.
11. Emit Human View.
12. Emit Machine View.
13. Validate both views agree.
14. **STOP**.

## Hard boundaries

Do not:
- render the final design;
- generate the final image;
- create ComfyUI graphs;
- create Figma nodes;
- write HTML/CSS/SVG/Remotion implementation;
- silently redesign the reference;
- invent unreadable text, exact fonts, exact colors, or dimensions;
- flatten semantic groups into unrelated objects;
- substitute vague style adjectives for measurable tokens.

## Completion test

The task is complete only when:
- material type is classified;
- major elements have semantic IDs;
- geometry uses normalized `{x,y,w,h}`;
- hierarchy is explicit;
- critical anchors/constraints are explicit;
- attention logic is explicit;
- style tokens are explicit;
- uncertainty is explicit;
- Human View and Machine View agree;
- no final asset has been generated.

After that, **STOP**.
