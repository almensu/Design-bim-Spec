# Canonical DRS Field Guide

The Design Reconstruction Specification (DRS) is the canonical intermediate representation between visual understanding and downstream rendering.

Executable JSON Schema:
`references/schema/design-reconstruction-spec.schema.json`

## Top level

```json
{
  "spec_version": "0.1.0",
  "mode": "reference_reconstruction",
  "material": {},
  "canvas": {},
  "style_tokens": {},
  "elements": [],
  "scene_graph": {},
  "anchors": [],
  "constraints": [],
  "attention_graph": {},
  "occlusion": [],
  "review": {}
}
```

## mode

- reference_reconstruction
- design_planning

## provenance

Every visually derived or planned value should distinguish:

- observed — directly supported by input;
- inferred — reasoned from visual/context evidence;
- proposed — a planning decision.

Never merge these silently.

## material

Example:

```json
{
  "category": "ecommerce_marketing",
  "type": "ecommerce_main_image",
  "intent": ["product_recognition", "conversion"],
  "confidence": 0.96
}
```

## canvas

Example:

```json
{
  "pixel_width": 1080,
  "pixel_height": 1350,
  "aspect_ratio": "4:5",
  "orientation": "portrait",
  "coordinate_system": {
    "origin": "top_left",
    "space": "normalized",
    "range": [0, 1],
    "bbox_format": "xywh"
  },
  "safe_area": {
    "left": 0.06,
    "right": 0.06,
    "top": 0.05,
    "bottom": 0.06,
    "source": "inferred",
    "confidence": 0.82
  }
}
```

## element

Each meaningful visible item is an element.

Required conceptual properties:
- stable semantic ID;
- role;
- bbox;
- layer depth;
- provenance;
- confidence.

Example:

```json
{
  "id": "product.main",
  "role": "product",
  "parent": "group.hero",
  "bbox": {"x":0.20,"y":0.18,"w":0.62,"h":0.48},
  "center": {"x":0.51,"y":0.42},
  "layer_depth": 30,
  "rotation_deg": 0,
  "source": "observed",
  "confidence": 0.95,
  "review_status": "accepted",
  "evidence": "Dominant central product silhouette is clearly visible."
}
```

## semantic IDs

Preferred:
- background.base
- group.hero
- product.main
- text.headline
- text.subtitle
- conversion.price
- conversion.badge
- conversion.cta
- proof.badge
- footer.legal

IDs should describe role, not appearance.

## scene_graph

Example:

```json
{
  "root": "canvas",
  "nodes": [
    {
      "id": "canvas",
      "type": "group",
      "children": ["background.base","group.hero","group.headline","group.conversion"]
    },
    {
      "id": "group.hero",
      "type": "group",
      "children": ["product.main","product.shadow"]
    }
  ]
}
```

Groups may be semantic even without a visible box.

## confidence

Range:
0.0–1.0

Suggested policy:
- 0.90–1.00 strong evidence;
- 0.70–0.89 usable with uncertainty;
- below 0.70 → needs_review.

Confidence must communicate uncertainty downstream.

## review

Example:

```json
{
  "needs_review": [
    {
      "path": "elements[text.headline].text",
      "reason": "Source image is too low resolution to read the final characters."
    }
  ],
  "notes": [
    "Price geometry is reliable; exact font family is uncertain."
  ]
}
```

## canonical vs auxiliary

Canonical:
- semantics;
- normalized geometry;
- hierarchy;
- anchors;
- constraints;
- attention;
- style tokens;
- provenance;
- confidence.

Auxiliary:
- raw OCR boxes;
- pixel coordinates;
- model-specific embeddings;
- renderer-specific prompt fragments.

Auxiliary data must not redefine canonical meaning.
