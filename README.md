# Design BIM Spec

**Design BIM Spec** is a multimodal design-analysis skill that converts a reference design or a design brief into a canonical, parameterized reconstruction specification.

It does **not** render the final artwork.

Its job is to:

```text
SEE
→ UNDERSTAND
→ CLASSIFY
→ DECOMPOSE
→ PARAMETERIZE
→ SPECIFY
→ STOP
```

The resulting specification is intended to be consumed by downstream models or tools such as image generators, ComfyUI workflows, layout models, HTML/CSS renderers, Figma automation, SVG/Canvas code, or motion-design systems.

## Core idea

Treat a 2D design like BIM treats a building:

- identify semantic objects rather than merely tracing pixels;
- represent every object in a normalized coordinate system;
- preserve parent/child grouping and layer depth;
- describe anchors, constraints, alignment, spacing, and occlusion;
- encode visual attention as a directed graph;
- extract reusable style tokens;
- distinguish observed facts from proposed layout decisions;
- attach confidence to uncertain observations.

The canonical representation is **Design Reconstruction Specification (DRS)**.

## Two operating modes

1. **Reference Reconstruction**
   - Input: one or more reference images.
   - Goal: explain what is visibly present and how the design is constructed.
   - Spatial values are primarily `observed`.

2. **Design Planning**
   - Input: a brief without a complete reference image.
   - Goal: propose a parameterized layout appropriate to the recognized material type.
   - Spatial values are primarily `proposed`.

## Output

Every successful run produces two synchronized views of the same design:

### Human View
A readable explanation for review:
- material recognition;
- design intent;
- visual hierarchy;
- eye-tracking path;
- layer stack;
- grouping;
- spatial relationships;
- anchors and constraints;
- style system;
- uncertainties and reconstruction notes.

### Machine View
A canonical JSON document containing:
- metadata;
- canvas and safe area;
- material classification;
- style tokens;
- elements and normalized bounding boxes;
- scene graph;
- anchors;
- constraints;
- attention graph;
- occlusion relationships;
- evidence/source markers;
- confidence and review flags.

## Coordinate convention

All canonical element bounds use:

```text
origin: top-left
coordinate_space: normalized
range: 0.0–1.0
bbox: { x, y, w, h }
```

Avoid ambiguous `[ymin, xmin, ymax, xmax]` arrays in the canonical form.

## Repository structure

```text
.
├── SKILL.md
├── AGENTS.md
├── schemas/
│   └── design-reconstruction-spec.schema.json
├── references/
│   ├── material-taxonomy.md
│   ├── visual-analysis-protocol.md
│   ├── canonical-schema.md
│   ├── layout-constraints.md
│   └── style-tokens.md
└── examples/
    ├── ecommerce-main-image/
    │   ├── human-spec.md
    │   └── machine-spec.json
    └── flyer/
        ├── human-spec.md
        └── machine-spec.json
```

## Non-goals

This skill must **not**:
- render the final asset;
- silently redesign a reference image;
- hallucinate exact text, dimensions, brand assets, or colors when evidence is weak;
- replace uncertainty with confident guesses;
- collapse all elements into a flat list without semantic grouping;
- use vague adjectives such as “premium” or “modern” as substitutes for measurable style properties.

## Principle

> Do not ask the downstream model to “draw something similar.” First compile the design into an explicit model of objects, geometry, hierarchy, constraints, attention, and style; then let the downstream model execute that model.
