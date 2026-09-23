# Output Contract

Every completed skill run returns two synchronized views.

## A. Human View

Use this structure:

```markdown
# Design Reconstruction Specification — Human View

## 1. Material Recognition
- Category
- Type
- Mode
- Canvas
- Aspect ratio
- Primary intent
- Confidence

## 2. Design Intent
What should the viewer notice, understand, and do?

## 3. Visual Attention Path
First fixation → subsequent fixations → terminal action.
Explain mechanisms.

## 4. Layer Stack
Back-to-front order.

## 5. Semantic Groups
Hero, headline, conversion, proof, footer, etc.

## 6. Spatial Layout
Regions, occupancy, whitespace, balance, alignment.

## 7. Anchors and Constraints
Explain dependency relationships in human language.

## 8. Style System
Palette, typography, spacing, radii, strokes, shadows, image treatment, lighting.

## 9. Occlusion and Cropping
Overlap, clipping, masks, edge crop, depth cues.

## 10. Uncertainty / Needs Review
Explicitly list low-confidence observations.

## 11. Reconstruction Notes
Only the guidance downstream execution needs.
```

## B. Machine View

Return one DRS JSON object conforming to:
`references/schema/design-reconstruction-spec.schema.json`

## Synchronization requirement

Human and Machine views must agree on:
- material classification;
- mode;
- major element identity;
- hierarchy;
- major coordinates;
- layer order;
- attention order;
- constraints;
- uncertainties.

If prose and JSON conflict, the task is not complete.

## Completion boundary

After both views are emitted:

```text
STOP
```

Do not:
- render;
- generate the final artwork;
- write implementation code;
- produce ComfyUI graphs;
- create Figma nodes;
- export SVG;
- generate Remotion;
- silently redesign.

Those are downstream responsibilities unless separately requested in another task.
