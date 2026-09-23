# Reference Index

Design BIM Spec follows a **thin SKILL / thick references** architecture.

The main `SKILL.md` is intentionally short. Detailed domain rules live here.

## Read first

| File | Responsibility |
|---|---|
| `material-taxonomy.md` | Controlled design-material classification |
| `visual-analysis-protocol.md` | Multimodal inspection sequence |
| `canonical-schema.md` | DRS semantic field definitions |
| `output-contract.md` | Human + Machine output contract |

## Read when needed

| File | Responsibility |
|---|---|
| `layout-constraints.md` | Coordinates, bbox, safe area, anchors, constraints, depth, crop, occlusion |
| `attention-model.md` | Fixations, salience mechanisms, transitions |
| `style-tokens.md` | Palette, typography, spacing, radius, shadows, lighting, image treatment |

## Executable contract

`schema/design-reconstruction-spec.schema.json`

This validates the canonical Machine View.

## Examples

`examples/ecommerce-main-image/`

`examples/flyer/`

Examples are illustrative, not templates to copy mechanically. The visual evidence always has priority.
