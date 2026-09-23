# Reference Index

Design BIM Spec follows a **thin SKILL / thick references** architecture.

The main `SKILL.md` is intentionally short. Detailed domain rules live here.

## Read first for a normal DRS task

| File | Responsibility |
|---|---|
| `material-taxonomy.md` | Controlled design-material classification |
| `visual-analysis-protocol.md` | Multimodal inspection sequence |
| `canonical-schema.md` | DRS semantic field definitions |
| `output-contract.md` | Human + Machine output contract |

## Read when needed during analysis

| File | Responsibility |
|---|---|
| `layout-constraints.md` | Coordinates, bbox, safe area, anchors, constraints, depth, crop, occlusion |
| `attention-model.md` | Fixations, salience mechanisms, transitions |
| `style-tokens.md` | Palette, typography, spacing, radius, shadows, lighting, image treatment |

## Read before accepting an output

| File | Responsibility |
|---|---|
| `Gotchas.md` | Task-routed repeated/high-cost failure patterns |
| `review-checklists/drs-output-review.md` | Human/Machine reconciliation and semantic-integrity review |

Do not treat JSON Schema success as complete acceptance.

## Learning & Evolution

These files are for **explicit repository maintenance**, not ordinary DRS generation.

| File | Responsibility |
|---|---|
| `evolution-loop.md` | Decide whether a lesson stays local, becomes a Gotcha/checklist/gate, or is retired |
| `improvement-record-template.md` | Freeze baseline, candidate, evaluation, results, limitations, and later-task evidence |
| `recursive-self-improvement-protocol.md` | Evidence requirements for L0/L1/L2 improvement claims |
| `changelog.md` | Maintain evidence-based English + Simplified Chinese changelogs |

### Learning route

```text
task evidence
→ improvement record
→ Gotcha
→ checklist
→ schema / validator / regression fixture
→ entrypoint routing only if necessary
→ later-task verification
→ guarded / retired / split
```

A rule landing in the repository makes it retrievable; it does not by itself prove benefit.

## Executable contract

`schema/design-reconstruction-spec.schema.json`

This validates the canonical Machine View structure.

Cross-ID references and other semantic integrity checks still require review or a dedicated validator.

## Examples

`examples/ecommerce-main-image/`

`examples/flyer/`

Examples are illustrative, not templates to copy mechanically. Visual evidence always has priority.

## Root records

- `../CHANGELOG.md` — English source of truth for repository change history.
- `../CHANGELOG.zh-CN.md` — Simplified Chinese mirror.
- `../docs/decisions/recursive-self-improvement-bootstrap.md` — initial learning-system baseline and claim boundary.
