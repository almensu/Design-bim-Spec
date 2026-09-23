# AGENTS.md

## Repository purpose

This repository defines a canonical multimodal skill for compiling 2D visual designs into a parameterized **Design Reconstruction Specification (DRS)**.

The repository is specification-first. Avoid turning it into a renderer.

## Invariants

Any contributor or agent editing this repository must preserve these invariants:

1. **Analysis before generation**
   - The skill analyzes and specifies.
   - It does not create the final artwork.

2. **Semantic decomposition over pixel tracing**
   - Prefer product, headline, price, CTA, badge, group, etc.
   - Raw pixel geometry is evidence, not the final representation.

3. **Normalized geometry**
   - Canonical bbox form is:
     `{ "x": 0.0, "y": 0.0, "w": 1.0, "h": 1.0 }`
   - Origin is top-left.

4. **Hierarchy matters**
   - Preserve semantic groups and parent/child relationships.

5. **Relations matter more than isolated coordinates**
   - Use anchors and constraints to explain layout behavior.

6. **Observed ≠ inferred ≠ proposed**
   - Never silently merge these evidence classes.

7. **Uncertainty is data**
   - Confidence and review flags are part of the canonical model.

8. **Human View and Machine View are two views of one model**
   - They must not contradict one another.

9. **Material taxonomy is controlled**
   - Normal execution does not invent arbitrary canonical material types.
   - Taxonomy expansion is a schema/versioning change.

10. **Backward compatibility**
   - Schema-breaking changes require a spec-version change and updated examples.

## Change checklist

When changing the canonical data model:
- update `schemas/design-reconstruction-spec.schema.json`;
- update `references/canonical-schema.md`;
- update `SKILL.md` if execution behavior changes;
- update at least one example;
- document new enums and semantics.

## Out of scope

Do not add:
- image-generation prompts that bypass the canonical spec;
- renderer-specific hacks as required core fields;
- undocumented magic coordinates;
- hard-coded brand styles;
- one-off schemas for individual posters.

Renderer adapters may be added later as optional consumers of DRS, but must not redefine the canonical model.
