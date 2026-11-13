---
tags: [textures, kit]
---

# 📦 Texture Kit

> [!summary]
> Seven original, tileable textures (22 PNGs, 512 × 512, made for this vault — free to use and modify) in `99 Assets/Textures/Kit/`. Normal maps are **OpenGL**. File suffixes: `_ALB` colour · `_NOR` normal · `_RGH` roughness · `_OVERLAY` transparent overlay · `_BAKED` grey with baked light.

![[tex-kit-sheet.jpg]]

| Folder | Files | StudsPerTile | Colour | Use for | Kit preview |
|---|---|--:|---|---|---|
| `studs/` | ALB · NOR · RGH · OVERLAY · BAKED | 2 | tint with Part.Color | classic studs (floors, bricks, walls) | ![[studs_OVERLAY.png\|72]] |
| `inlets/` | OVERLAY · NOR | 2 | tint | classic undersides | ![[inlets_OVERLAY.png\|72]] |
| `checker-grass/` | ALB · NOR · RGH | 8 | full colour | lanes, obby floors, simulator ground | ![[checker-grass_ALB.png\|72]] |
| `checker-dirt/` | ALB · NOR · RGH | 8 | full colour | walls, cliffs, borders | ![[checker-dirt_ALB.png\|72]] |
| `wood-planks/` | ALB · NOR · RGH | 8 | full colour | docks, decks, crates | ![[wood-planks_ALB.png\|72]] |
| `bricks/` | ALB · NOR · RGH | 6 | full colour | bases, houses | ![[bricks_ALB.png\|72]] |
| `arena-tiles/` | ALB · NOR · RGH | 8 | tint | competitive arenas, labs | ![[arena-tiles_ALB.png\|72]] |

## Use it

1. **Upload**: Studio → Asset Manager → Import (or Creator Hub → Development Items → Images/Decals). Note each asset ID.
2. **As a MaterialVariant** (light-reactive, any part): [[Playbook - Custom Materials with MaterialService]].
3. **As a Texture** (stud overlay on top faces): [[Playbook - Stud Texture#Method 2 — Texture overlay (any part colour)]].
4. **On meshes**: put `_ALB` / `_NOR` / `_RGH` into a `SurfaceAppearance` (the mesh's UVs must be laid out to tile).

## Every map in the kit

> [!gallery]- studs (5 maps)
> ![[studs_ALB.png]] ![[studs_BAKED.png]] ![[studs_NOR.png]] ![[studs_OVERLAY.png]] ![[studs_RGH.png]]

> [!gallery]- inlets (2 maps)
> ![[inlets_NOR.png]] ![[inlets_OVERLAY.png]]

> [!gallery]- checker-grass (3 maps)
> ![[checker-grass_ALB.png]] ![[checker-grass_NOR.png]] ![[checker-grass_RGH.png]]

> [!gallery]- checker-dirt (3 maps)
> ![[checker-dirt_ALB.png]] ![[checker-dirt_NOR.png]] ![[checker-dirt_RGH.png]]

> [!gallery]- wood-planks (3 maps)
> ![[wood-planks_ALB.png]] ![[wood-planks_NOR.png]] ![[wood-planks_RGH.png]]

> [!gallery]- bricks (3 maps)
> ![[bricks_ALB.png]] ![[bricks_NOR.png]] ![[bricks_RGH.png]]

> [!gallery]- arena-tiles (3 maps)
> ![[arena-tiles_ALB.png]] ![[arena-tiles_NOR.png]] ![[arena-tiles_RGH.png]]

## Previews

![[tex-studs-methods.jpg]]
![[tex-materials-gallery.jpg]]
![[tex-classic-scene.jpg]]

> [!note] Where these came from
> Generated procedurally for this vault (distance fields + tileable sine noise; normals computed from height maps) — the same steps as [[Playbook - Making Tileable Textures]], done in code.
