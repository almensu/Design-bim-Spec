# Visual Attention Model

DRS models visual attention as a **directed graph**, not merely a ranked list.

It is an inferred design model, not laboratory eye-tracking data.

## Fixations

Each major fixation includes:

```json
{
  "rank": 1,
  "target": "product.main",
  "weight": 1.0,
  "mechanisms": ["scale", "centrality", "contrast"],
  "confidence": 0.90
}
```

## Weight

Weights are relative within a single composition.

Suggested interpretation:
- 1.00: dominant;
- 0.75–0.99: strong secondary;
- 0.50–0.74: supporting;
- below 0.50: low-salience/supporting detail.

Do not imply physiological precision.

## Salience mechanisms

Canonical vocabulary:
- scale
- luminance_contrast
- color_contrast
- saturation
- isolation
- whitespace
- centrality
- edge_position
- face
- gaze
- directional_cue
- diagonal
- repetition
- type_scale
- font_weight
- enclosure
- proximity
- alignment
- depth
- blur_sharpness
- motion_cue

## Transitions

Represent why attention moves from A to B:

```json
{
  "from": "text.headline",
  "to": "conversion.price",
  "mechanisms": ["alignment", "proximity", "color_contrast"],
  "confidence": 0.84
}
```

## Terminal action

When the material has a conversion action, mark the likely terminal action region:
- CTA;
- QR;
- contact;
- purchase cue.

Do not manufacture a CTA when none exists.

## Reading direction

Reading direction can influence interpretation but must not override actual salience.

Possible metadata:
- ltr
- rtl
- vertical
- mixed
- unknown

## Human View wording

Explain attention as:
1. first fixation;
2. secondary fixation;
3. progression;
4. terminal action;
5. mechanisms.

Example:

> The product wins the first fixation through scale and isolation. The headline is the second fixation because it occupies the strongest high-contrast type block. Alignment and proximity then move attention into the price block and CTA.

## Anti-pattern

Do not always write:

```text
product → headline → CTA
```

A poster may actually be:
```text
headline → date → hero image → QR
```

A discount creative may be:
```text
price → product → CTA
```

Follow the evidence.
