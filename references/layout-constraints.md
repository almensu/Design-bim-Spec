# Layout, Anchors & Constraints

This reference defines spatial relationships in DRS.

## Coordinate system

Canonical space:

```text
origin = top-left
x increases → right
y increases ↓ down
range = 0.0–1.0
bbox = {x, y, w, h}
```

Example:

```json
{
  "x": 0.10,
  "y": 0.20,
  "w": 0.80,
  "h": 0.50
}
```

## Why bbox is not enough

A bbox records **where an element currently is**.

A constraint records **why it stays there**.

Both are required for faithful reconstruction and responsive adaptation.

## Standard anchors

- top
- bottom
- left
- right
- center
- top_left
- top_right
- bottom_left
- bottom_right
- baseline
- visual_center

## Anchor relationship

Example:

```json
{
  "id": "anchor.badge_to_product",
  "from": {
    "element": "conversion.badge",
    "anchor": "center"
  },
  "to": {
    "element": "product.main",
    "anchor": "top_right"
  },
  "offset": {
    "x": -0.03,
    "y": 0.02
  },
  "source": "inferred",
  "confidence": 0.88
}
```

## Canonical constraint types

### Alignment
- align_left
- align_right
- align_center_x
- align_top
- align_bottom
- align_center_y
- baseline_align

### Directional
- above
- below
- left_of
- right_of

### Containment
- inside
- contains
- stay_inside_safe_area

### Spacing
- gap
- min_gap
- max_gap
- equal_gap
- edge_offset

### Geometry
- maintain_aspect_ratio
- equal_width
- equal_height
- proportional_scale

### Collision
- avoid_overlap

### Attachment
- attach

## Constraint priority

- required
- strong
- medium
- weak

Use `required` only when breaking the relationship would visibly break the design.

## Safe area

Represent safe area as normalized margins:

```json
{
  "left": 0.06,
  "right": 0.06,
  "top": 0.05,
  "bottom": 0.06
}
```

Typical protected elements:
- logo;
- headline;
- CTA;
- legal copy;
- key price/value.

Decorative elements may intentionally cross the safe area.

## Layer depth

Use integer depth values with larger numbers closer to the viewer.

Suggested bands:
- 0–9: background;
- 10–19: background decoration;
- 20–39: main imagery/product;
- 40–59: foreground decoration/effects;
- 60–79: primary text;
- 80–89: conversion UI/badges;
- 90–99: overlays/critical labels.

Bands are conventions, not a replacement for observed occlusion.

## Crop

Record canvas crop explicitly:

```json
{
  "left": false,
  "right": true,
  "top": false,
  "bottom": false
}
```

Do not force cropped elements back inside the canvas.

## Occlusion

Represent pairwise visible relationships:

```json
{
  "front": "product.main",
  "behind": "decorative.arc_1",
  "relation": "overlap",
  "source": "observed",
  "confidence": 0.97
}
```

Supported relation vocabulary:
- overlap
- mask
- clip
- behind
- in_front_of

## Responsive implication

When adapting aspect ratio, preserve in this order unless evidence says otherwise:
1. semantic groups;
2. required anchors;
3. required constraints;
4. attention hierarchy;
5. safe area;
6. relative scale;
7. absolute normalized positions.

This prevents “coordinate copying” from destroying design logic.
