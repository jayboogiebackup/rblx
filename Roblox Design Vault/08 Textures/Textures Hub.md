---
tags: [textures, moc]
---

# 🎨 Textures Hub — textures, materials & the stud texture

> [!abstract] What's in this section
> How the top games texture their worlds (the **classic stud and checkerboard look** is back in the newest hits), which Roblox object to use for which job, how to make **tileable PBR textures**, how to set up **custom materials**, and a free **Texture Kit** (studs, inlets, checker grass, checker dirt, wood planks, bricks, arena tiles).

![[tex-studs-methods.jpg]]

## Start here

| Page | What you get |
|---|---|
| [[Texture Styles in Top Games]] | Official close-ups: TFFA checkerboards, Brainrot studs, RIVALS tiles, Fish It planks… |
| [[Texture Objects & Specs]] | Decal vs Texture vs MaterialVariant vs SurfaceAppearance vs TextureID; sizes, formats, tinting |
| [[Playbook - Stud Texture]] | Four ways to get studs, step by step, with settings and code |
| [[Playbook - Making Tileable Textures]] | Make your own seamless colour/normal/roughness sets (Krita/GIMP/Blender) |
| [[Playbook - Custom Materials with MaterialService]] | Turn a texture set into a material for parts (and terrain) |
| [[Texture Kit]] | 7 original tileable textures (22 PNGs) ready to upload |
| [[Template - Texture Spec]] | One-page spec before you paint |

![[tex-classic-scene.jpg]]

## 12 rules for textures in top Roblox games

1. **Pick one surface language per game** — studs, checkerboard, clean tiles, painted wood or realistic PBR — and use it everywhere.
2. **Studs and checkers read as 'Roblox'** — 🔎 [[Throw Food For Animals]] and [[Steal a Brainrot]] lean into the classic look on purpose (nostalgia + instant readability).
3. **Tint, don't duplicate** — one light-grey map × part colour gives every colour (MaterialVariant / Texture `Color3` / SurfaceAppearance `Color`).
4. **Match `StudsPerTile` to the image** — a tile with 2 × 2 studs needs StudsPerTile 2 for real 1-stud spacing. ![[tex-tiling.jpg]]
5. **Use a normal map for light-reactive detail** (studs, grooves, planks) instead of real geometry.
6. **Normal maps are OpenGL** (green = up).
7. **512² is plenty for tiling textures; 1024² is the cap** — uploads above it are downscaled.
8. **Seamless or nothing** — test every texture tiled 3 × 3 before uploading.
9. **Big shapes, low contrast** for floors players stare at; save contrast for gameplay surfaces (lanes, goals, hazards).
10. **Checkers mark progress** — change the checker colours per zone (🔎 TFFA's biome blocks).
11. **Don't fake geometry you can see edge-on** — a normal-mapped stud looks flat at grazing angles; that's fine for floors, not for silhouettes.
12. **Reuse a small kit** — 6–10 materials can texture a whole simulator map.

Related: [[Models Hub]] · [[Art Style]] · [[Color Palettes]] · [[Maps & World Building]]
