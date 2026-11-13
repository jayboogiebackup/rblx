---
tags: [playbook, textures]
---

# 🛠️ Playbook — Making Tileable Textures

> [!summary] Goal
> Make seamless **colour + normal + roughness** sets for floors, walls and props — like the [[Texture Kit]]'s checker grass, wood planks and bricks — with free tools.

![[tex-kit-sheet.jpg]]

## Tools

| Tool | Free? | Best for |
|---|:--:|---|
| **Krita** | ✅ | painting; wrap-around mode; *Height to Normal Map* filter |
| **GIMP** | ✅ | offset/tiling checks; *Normal Map* filter |
| **Blender** | ✅ | baking normal/roughness from geometry; procedural textures |
| **Material Maker** | ✅ | node-based procedural materials (like Substance Designer) |
| Photoshop / Substance | paid | painting; procedural PBR |

## Step 1 — Decide scale (texel density)

Pick one density for the whole kit, e.g. **512 px = 8 studs (64 px per stud)**. Then every texture's `StudsPerTile` follows from what it shows:

| Texture | What the 512² image shows | StudsPerTile |
|---|---|--:|
| checker grass / dirt | 2 × 2 cells of 4 studs | 8 |
| wood planks | 4 planks, each 2 studs wide | 8 |
| bricks | 8 rows × 2 bricks (kit default 6 = chunkier bricks; 8 = 1-stud-tall bricks) | 6–8 |
| arena tiles | 2 × 2 tiles of 4 studs | 8 |
| studs | 2 × 2 studs | 2 |

## Step 2 — Block the pattern on a grid that divides the canvas

Checkers, planks and bricks must repeat an **exact** number of times across 512 px (2, 4, 8 …) or the edges won't meet.

## Step 3 — Make it seamless

- **GIMP**: *Layer → Transform → Offset* by (256, 256) → paint over any seam in the middle → offset back.
- **Krita**: press **W** for wrap-around mode and paint across edges directly.
- Avoid unique features (a single knot in the wood) — they reveal the repeat.

## Step 4 — Height map → normal map

1. Paint a **greyscale height** layer: white = raised (tile tops, brick faces), black = low (grout, gaps).
2. Generate the normal map: Krita *Filter → Edge Detection → Height to Normal Map*, or GIMP *Filters → Generic → Normal Map*.
3. Roblox expects **OpenGL** normals (green = up). If yours look inverted (lit from below), flip the green channel.
4. Keep strength modest — exaggerated normals look plastic and shimmer at distance.

## Step 5 — Roughness (and metalness)

Greyscale: **white = rough, black = glossy**. Grout and dirt rough; tile tops and varnished wood smoother. Metalness only for real metal (black everywhere else).

## Step 6 — Colour map

- **For PBR**: no baked lighting or shadows — the engine lights it from the normal map.
- **For tintable textures** (studs, tiles): keep it light grey so `Part.Color` / `SurfaceAppearance.Color` can tint it.
- Low contrast on surfaces players stare at; saturate only gameplay surfaces.

## Step 7 — Test before uploading

- Tile 3 × 3 in your editor: any seams? any obvious repeats?
- Shrink to 25%: does it turn to mush or moiré? Reduce fine detail if so.
- Apply in Studio on a 40 × 40-stud floor and walk it on a phone.

## Step 8 — Export & name

PNG, 512² (1024² max — larger is downscaled). Name by map: `name_ALB.png`, `name_NOR.png`, `name_RGH.png` (`_MET` for metalness). Upload via Asset Manager → Import, then use in a [[Playbook - Custom Materials with MaterialService|MaterialVariant]] or `Texture`.

## Recipes (how the kit was made)

| Texture | Height | Colour | Roughness |
|---|---|---|---|
| Checker grass | raised square cells with 10 px bevels | two greens (#6BD64F / #55C03C) + soft noise | 0.85 |
| Checker dirt | cells + small 64 px sub-squares | two browns (#A8703F / #8F5C31) | 0.9 |
| Wood planks | 4 planks, 4 px gaps, staggered seams, nails | 4 plank tones × wavy grain | 0.6–0.7 |
| Bricks | running bond, 6 px mortar | 5 red tones + noise, mortar #D9CFC0 | 0.75–0.8 |
| Arena tiles | 3 px grout, '+' markers at corners | pale lavender #E6E8F6, grout #C6CBE9 | 0.35 tiles / 0.65 grout |
| Studs | circles radius 30% of cell, soft edge | flat light grey | 0.45–0.55 |

> [!tip] Hide repetition on big natural surfaces
> Set a MaterialVariant's `Pattern = Organic` to break up obvious tiling on grass, sand or rock; keep `Regular` for man-made patterns (checkers, tiles, bricks, studs).

Related: [[Playbook - Stud Texture]] · [[Texture Objects & Specs]] · [[Textures Hub]]
