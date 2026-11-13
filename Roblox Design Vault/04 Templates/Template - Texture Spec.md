---
tags: [template, textures]
surface: "" # floor · wall · prop · mesh
style: "" # studs · checkerboard · tiles · wood · realistic
object: "" # Texture · MaterialVariant · SurfaceAppearance · TextureID · Decal
---

# Texture Spec — {{title}}

Reference: [[Texture Objects & Specs]] · [[Playbook - Making Tileable Textures]] · [[Textures Hub]]

| Field | Value |
|---|---|
| What it covers (studs × studs) | |
| Image size | 512² (max 1024²) |
| What one tile shows | e.g. 2 × 2 studs / 4 planks |
| StudsPerTile | |
| Maps | ALB · NOR (OpenGL) · RGH · MET |
| Tintable? | light-grey ALB → yes |
| Pattern | Regular / Organic |
| Base material (if MaterialVariant) | |

## Checks
- [ ] Seamless when tiled 3 × 3
- [ ] Readable at gameplay distance on a phone (no moiré)
- [ ] Matches the game's surface language and palette ([[Color Palettes]])
- [ ] Asset IDs recorded below

| Map | Asset ID |
|---|---|
| ALB | |
| NOR | |
| RGH | |
