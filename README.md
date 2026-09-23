# Design BIM Spec

**Design BIM Spec** compiles a reference design image or design brief into a canonical **Design Reconstruction Specification (DRS)**.

It is designed for multimodal models with visual understanding.

It does **not** render the final artwork.

```text
SEE
→ UNDERSTAND
→ CLASSIFY
→ DECOMPOSE
→ PARAMETERIZE
→ SPECIFY
→ STOP
```

## Why “BIM” for graphic design?

The skill treats a 2D design as a structured spatial model rather than a flat image:

- semantic objects instead of raw pixel fragments;
- normalized X–Y geometry;
- semantic groups and parent/child hierarchy;
- anchors and constraints;
- layer depth, crop, and occlusion;
- visual-attention graph;
- measurable style tokens;
- explicit uncertainty and provenance.

The goal is to let downstream systems **rebuild from a specification**, rather than “look at the reference and draw something similar.”

## Architecture

This repository intentionally uses a **thin SKILL / thick references** architecture.

```text
.
├── README.md
├── AGENTS.md
├── SKILL.md
└── references/
    ├── reference-index.md
    ├── material-taxonomy.md
    ├── visual-analysis-protocol.md
    ├── canonical-schema.md
    ├── layout-constraints.md
    ├── attention-model.md
    ├── style-tokens.md
    ├── output-contract.md
    ├── schema/
    │   └── design-reconstruction-spec.schema.json
    └── examples/
        ├── ecommerce-main-image/
        │   ├── human-spec.md
        │   └── machine-spec.json
        └── flyer/
            ├── human-spec.md
            └── machine-spec.json
```

`SKILL.md` contains only:
- responsibility;
- mode selection;
- reference routing;
- execution order;
- hard boundaries;
- completion test.

All domain details live under `references/`.

## Two modes

### reference_reconstruction
Use when a reference image exists.

Values should be labeled:
- `observed`
- `inferred`

### design_planning
Use when a brief exists without a complete reference layout.

Layout decisions should be labeled:
- `proposed`

## Canonical output

Each run produces two synchronized views:

1. **Human View** — a readable explanation of spatial and visual logic.
2. **Machine View** — a DRS JSON object.

The Machine View is validated against:

`references/schema/design-reconstruction-spec.schema.json`

## Coordinate convention

```text
origin = top-left
coordinate space = normalized
range = 0.0–1.0
bbox = {x, y, w, h}
```

## Core material taxonomy v0.1

### Ecommerce
- ecommerce_main_image
- pdp_hero
- livestream_background
- feed_ad

### Offline
- dm_leaflet_or_fold
- marketing_poster
- flyer

Unsupported or ambiguous inputs use `unknown`; execution does not silently invent canonical material types.

## Downstream consumers

DRS can be consumed by:
- multimodal/image-generation models;
- ComfyUI pipelines;
- layout models;
- HTML/CSS;
- SVG/Canvas;
- Figma automation;
- Remotion;
- other renderers.

Those systems are downstream. This repository ends at specification.

## Core principle

> First compile the design into objects, geometry, hierarchy, constraints, attention, and style. Then let another model or renderer execute the specification.
