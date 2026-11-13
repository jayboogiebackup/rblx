---
tags: [textures, reference, specs]
---

# 📐 Texture Objects & Specs

> [!summary]
> Roblox has six ways to put an image on something. Choose by **what** you're texturing (part face, whole part, mesh with UVs) and **whether** it must tile, react to light, or be tinted.

![[tex-objects-diagram.jpg]]

## The six objects

| Object | Goes on | Tiles? | Lit by normal map? | Tint | Key properties |
|---|---|:--:|:--:|---|---|
| **Decal** | one face of a part | ✖ stretches | ✖ | `Color3` | `Texture`, `Face`, `Transparency`, `ZIndex` |
| **Texture** | one face of a part | ✔ | ✖ | `Color3` | `StudsPerTileU/V`, `OffsetStudsU/V`, `Face` |
| **MaterialVariant** | parts (per-part or global override) and terrain materials | ✔ | ✔ | `Part.Color` | `ColorMap`, `NormalMap`, `RoughnessMap`, `MetalnessMap`, `StudsPerTile`, `Pattern`, `BaseMaterial` |
| **SurfaceAppearance** | a MeshPart (uses its UVs) | via UVs | ✔ | `Color` | `ColorMap`, `NormalMap`, `RoughnessMap`, `MetalnessMap`, `AlphaMode` |
| **MeshPart.TextureID** | a MeshPart | via UVs | ✖ | — | one colour texture |
| **SurfaceType Studs** (legacy) | part faces | ✔ | built-in | `Part.Color` | `TopSurface`, `BottomSurface`… (deprecated) |

> [!info] Notes from the docs and DevForum
> - **Texture**: "Unlike Decals, the texture… will repeat when the parent BasePart is resized"; `StudsPerTileU/V` set the tile size and `OffsetStudsU/V` can be tweened for animated surfaces (conveyors, water) — Roblox docs.
> - **MaterialVariant** only works inside **MaterialService**; assign it per part with `BasePart.MaterialVariant = "Name"` or globally with `MaterialService:SetBaseMaterialOverride(Enum.Material.X, "Name")`. The variant's `BaseMaterial` must match the slot. `StudsPerTile` sets scale; `Pattern` is `Regular` or `Organic` — Roblox docs.
> - **SurfaceAppearance.Color** multiplies the colour map (use light-grey maps for the widest range); `AlphaMode = TintMask` tints only where the ColorMap alpha is opaque — DevForum release notes (TintMask announced as a client beta; check its status).
> - **SurfaceType Studs** is deprecated (the Surface tool was removed), but setting `Part.TopSurface = Enum.SurfaceType.Studs` from a script still works per DevForum reports. Use Textures or MaterialVariants for new work.

## Specs

| Spec | Value | Source |
|---|---|---|
| Max image size | **1024 × 1024** (larger uploads are downscaled) | DevForum |
| PBR maps (SurfaceAppearance) | up to 1024 × 1024 | Roblox texture specifications |
| Normal maps | **OpenGL, tangent space** | Roblox docs |
| Formats | PNG, JPG/JPEG, BMP (GIF uploads become static); convert EXR/TGA first | Roblox docs + DevForum |
| Alpha | needs a format with an alpha channel (PNG) | guides |
| Naming used in Roblox docs | `_ALB` colour · `_NOR` normal · `_MET` metalness · roughness map | Roblox texture specifications |

## Recommended sizes (🧠 guideline)

| Use | Size |
|---|---|
| Tiling floor / wall material | 512² (1024² for hero surfaces) |
| Stud / checker pattern | 256–512² |
| Palette for voxel / low-poly | 64² (cells ≥ 16 px) |
| Pet / weapon SurfaceAppearance | 512² (heroes 1024²) |
| Decals (signs, faces) | 256–512² |

## Performance

- **Reuse** the same texture IDs across parts — memory is per unique image.
- Prefer **one MaterialVariant** over hundreds of Texture objects on hundreds of parts.
- **Normal maps** replace real geometry (16 real studs = 1,024 extra triangles per brick — see [[tex-studs-methods.jpg]]).
- Keep tiny textures tiny — a 1024² image for a 2-stud sign wastes memory on phones.

Sources: [Roblox docs — Textures and decals](https://create.roblox.com/docs/parts/textures-decals) · [Roblox docs — MaterialVariant](https://create.roblox.com/docs/reference/engine/classes/MaterialVariant) · [Roblox docs — MaterialService](https://create.roblox.com/docs/reference/engine/classes/MaterialService) · [Roblox docs — Texture specifications](https://create.roblox.com/docs/art/modeling/texture-specifications) · [Roblox docs — PBR textures](https://create.roblox.com/docs/art/modeling/surface-appearance) · [DevForum — SurfaceAppearance tinting](https://devforum.roblox.com/t/full-release-surfaceappearance-tinting/3129960) · [DevForum — TintMask](https://devforum.roblox.com/t/client-beta-introducing-tintmask-for-surfaceappearance/3600497) · [DevForum — Deprecating Surface Tool API](https://devforum.roblox.com/t/deprecating-surface-tool-api/1222218) · [DevForum — Studs via TopSurface](https://devforum.roblox.com/t/how-to-change-a-parts-surface-to-studs-no-textures-or-decals-required/3497234) · [DevForum — max upload size](https://devforum.roblox.com/t/dramatically-increase-the-maximum-image-decal-texture-upload-size/649052)
