# Visual Analysis Protocol

This reference defines how a multimodal model inspects a design before writing the canonical spec.

## Pass 0 — Evidence quality

Record:
- source resolution;
- crop completeness;
- perspective distortion;
- compression/noise;
- readable/unreadable text;
- screenshot/export/photo/scan/mockup status.

Reduce confidence when evidence is weak.

## Pass 1 — Material recognition

Determine:
- category;
- canonical type;
- orientation;
- aspect ratio;
- likely medium;
- likely viewing context;
- communication intent.

Do not start micro-spacing analysis before material context is established.

## Pass 2 — Gestalt segmentation

Find coherent regions using:
- proximity;
- alignment;
- enclosure;
- shared background;
- similarity;
- repetition;
- continuation;
- typography consistency;
- color consistency.

The goal is to discover semantic groups before flattening objects.

## Pass 3 — Semantic objects

Prefer semantic identities:

```text
product.main
text.headline
conversion.price
conversion.cta
proof.badge
```

Avoid appearance-only identities such as `red_rectangle_1`.

Appearance belongs in properties; meaning belongs in IDs and roles.

## Pass 4 — Geometry

Estimate:
- normalized bbox;
- center;
- rotation;
- crop;
- relative scale;
- alignment;
- region occupancy.

Canonical coordinates are normalized even when pixels are available.

## Pass 5 — Depth and occlusion

Determine:
- front/behind;
- overlap;
- masks;
- clipping;
- shadows/glows;
- canvas-edge cropping.

Do not mistake an effect for an independent semantic object.

## Pass 6 — Scene graph

Ask:
- which objects move together?
- which object derives position from another?
- which elements form one communication unit?

Build groups such as:
- hero;
- headline;
- conversion;
- proof;
- footer.

## Pass 7 — Anchors

Recover dependency points:
- badge → product.top_right;
- subtitle → headline.bottom;
- CTA → price.bottom;
- logo → safe_area.top_left.

Use anchors to preserve design intent under resizing.

## Pass 8 — Constraints

Recover rules only when supported:
- align;
- above/below;
- left/right;
- inside;
- equal gap;
- min/max gap;
- safe-area containment;
- aspect-ratio preservation;
- avoid overlap.

Label each rule as observed, inferred, or proposed.

## Pass 9 — Attention

Estimate fixation order from visible salience.

Evidence:
- scale;
- contrast;
- saturation;
- isolation;
- whitespace;
- centrality;
- faces/gaze;
- directional cues;
- diagonals;
- repetition;
- motion cues.

Do not hard-code a universal product → headline → CTA order.

## Pass 10 — Style extraction

Translate aesthetics into measurable tokens:
- colors;
- type scale;
- font class;
- weight;
- tracking;
- line height;
- spacing rhythm;
- radius;
- strokes;
- shadows;
- gradients;
- image treatment;
- lighting;
- whitespace.

Words such as “premium” or “modern” may be summaries, never substitutes for tokens.

## Pass 11 — Text handling

If readable:
- preserve exact wording.

If partially readable:
- preserve supported spans;
- mark uncertainty.

If unreadable:
- use semantic placeholders;
- never fabricate copy.

## Pass 12 — Consistency check

Verify:
- all major visible groups are represented;
- bboxes are legal;
- hierarchy is coherent;
- layer order agrees with overlap;
- constraints agree with geometry;
- attention agrees with visual evidence;
- exactness is not overstated.

Then produce Human View and Machine View.
