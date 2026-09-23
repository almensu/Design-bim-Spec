# DRS Output Review Checklist

Use before accepting a Human View + Machine View pair.

This checklist is a human/agent judgment gate. It is not proof of later-task improvement.

## Material & Canvas

- [ ] Material type comes from the controlled taxonomy or is explicitly `unknown`.
- [ ] Mode is correct: `reference_reconstruction` or `design_planning`.
- [ ] Canvas/aspect ratio is supported by evidence or labeled proposed/inferred.
- [ ] Coordinate convention is normalized top-left `{x,y,w,h}`.

## Semantics & Hierarchy

- [ ] Major visible/required objects have semantic IDs.
- [ ] Related elements are grouped rather than flattened.
- [ ] Product/effect/text/UI roles are not confused.
- [ ] Renderer-specific IDs have not become canonical semantics.

## Geometry & Topology

- [ ] Critical elements have bboxes.
- [ ] Important relative positions also have anchors/constraints.
- [ ] Parent/child logic explains what should move together.
- [ ] Crop and occlusion agree with layer depth.

## Provenance & Uncertainty

- [ ] `observed`, `inferred`, and `proposed` are not conflated.
- [ ] Low-resolution evidence does not produce fake exactness.
- [ ] Unreadable copy uses placeholders/review flags instead of hallucinated wording.
- [ ] Exact font/color claims have sufficient evidence.

## Attention

- [ ] Fixation order is derived from visible salience, not a canned template.
- [ ] Transition mechanisms are named.
- [ ] No CTA/terminal action is invented when none exists.

## Style

- [ ] Style Tokens contain measurable/categorical properties.
- [ ] Mood adjectives do not replace palette/type/spacing/shadow properties.
- [ ] Lighting/image treatment is separated from layout geometry.

## Human ↔ Machine Reconciliation

- [ ] Material and mode agree.
- [ ] Major element identities agree.
- [ ] Visual hierarchy agrees.
- [ ] Layer stack agrees.
- [ ] Anchor/constraint explanations agree.
- [ ] Attention order agrees.
- [ ] Needs-review items agree.

## Semantic Integrity

JSON Schema success is not enough.

- [ ] Every scene graph child resolves.
- [ ] Every anchor endpoint resolves.
- [ ] Every constraint subject resolves.
- [ ] Every attention target resolves.
- [ ] Terminal action resolves when present.
- [ ] Occlusion references resolve.
- [ ] No obvious relation contradicts element geometry.

## Boundary

- [ ] Output stops at specification.
- [ ] No final image/render/code/Figma/ComfyUI graph was generated unless separately requested.
- [ ] Canonical DRS was not warped around one downstream renderer.

## Learning Check

If review fails:
- [ ] Preserve high-cost failure evidence before overwriting.
- [ ] Check relevant `Gotchas.md`.
- [ ] If repeated/high-cost, route through `evolution-loop.md`.
