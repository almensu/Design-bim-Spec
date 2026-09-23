# Style Tokens

Style Tokens encode reusable visual properties separately from geometry.

## Principle

Prefer measurable or categorical properties over vague adjectives.

Bad:
```text
premium, elegant, modern
```

Better:
```json
{
  "palette": {
    "background": "#F6F2EA",
    "text_primary": "#171717",
    "accent": "#D44A2C"
  },
  "typography": {
    "headline": {
      "font_class": "sans-serif",
      "weight": 700,
      "size_rel_h": 0.058
    }
  }
}
```

## Palette

Recommended roles:
- background;
- surface;
- text_primary;
- text_secondary;
- brand_primary;
- brand_secondary;
- accent;
- highlight;
- border;
- shadow_tint.

For uncertain colors store:
- estimated hex/RGB;
- source;
- confidence.

## Background

Recommended fields:
- type: solid | gradient | image | texture | composite;
- dominant_color;
- gradient direction;
- brightness distribution;
- texture density.

## Typography

Per semantic role:
- font_family if known;
- font_class if family unknown;
- weight;
- size relative to canvas width or height;
- line height;
- tracking;
- case;
- alignment;
- color;
- emphasis.

Suggested font classes:
- sans-serif
- serif
- display
- script
- monospace
- unknown

Do not hallucinate an exact font family from insufficient evidence.

## Spacing

Capture:
- base spacing unit;
- major section gaps;
- intra-group gaps;
- padding;
- whitespace ratio.

Relative units are preferred.

## Radius

Record:
- none;
- fixed normalized estimate;
- pill;
- circular.

## Stroke

Record:
- width;
- color;
- opacity;
- style.

## Shadow

Record:
- offset_x;
- offset_y;
- blur;
- spread if inferable;
- opacity;
- color/tint;
- softness.

## Glow

Record:
- radius;
- opacity;
- tint;
- falloff.

## Gradient

Record:
- type;
- direction/angle;
- color stops;
- opacity;
- source/confidence.

## Image treatment

Useful fields:
- crop mode;
- saturation;
- contrast;
- warmth;
- depth of field;
- blur;
- cutout vs environmental scene;
- edge softness;
- compositing mode.

## Lighting

Useful fields:
- dominant direction;
- key/fill relation;
- hardness;
- highlight direction;
- rim light;
- shadow direction.

Treat lighting as an image-treatment property, not a layout property.

## Density

Describe:
- information_density: low | medium | high;
- decorative_density: low | medium | high;
- whitespace_ratio: normalized estimate.

## Semantic style summary

Optional summaries like:
- technical;
- editorial;
- playful;
- restrained;
- luxury;
- youthful.

These are descriptive annotations only. They must never replace measurable tokens.
