---
tags: [textures, art, reference]
---

# 🔎 Texture Styles in Top Games

> [!summary]
> The newest chart-toppers bring back the **classic Roblox surface language** — studs and checkerboards — while competitive and roleplay games use **clean tiles** and **realistic materials**. Crops below are from official store images (© their creators), shown for study.

> [!note] Confidence legend
> 🔎 observed in official store images · 🧠 inference about how it was made

![[ref-textures.jpg]]

## Five surface languages

| Style | Seen in (🔎) | Look | How to reproduce | Kit texture |
|---|---|---|---|---|
| **Classic studs** | [[Steal a Brainrot]] ground, conveyor carpet and base walls | Raised round studs on every surface | Stud Texture overlay or studs MaterialVariant — [[Playbook - Stud Texture]] | `studs`, `inlets` |
| **Bright checkerboard** | [[Throw Food For Animals]] grass lane, dirt walls, biome blocks | Two-tone squares with small bevels; one colour pair per zone | Tileable checker texture (StudsPerTile = 2 × cell size) | `checker-grass`, `checker-dirt` |
| **Clean tiles + markers** | [[RIVALS]] walls and floors | Pale lavender/white tiles, thin grout, '+' markers | Tile texture, low roughness, tinted | `arena-tiles` |
| **Painted wood & props** | [[Fish It]] dock, [[99 Nights in the Forest]] log walls | Warm planks with gaps, cartoon grain | Plank texture with normal map | `wood-planks` |
| **Realistic PBR** | [[Brookhaven RP]] houses | Real brick, plaster, glass, roads | SurfaceAppearance / MaterialVariant with full PBR sets | `bricks` (stylised) |
| *(plus)* **Neon grid / void** | [[Steal An Egg]] space biome | Saturated purple floor with a glowing grid | Texture overlay with emissive-looking colours + Neon material accents | — |

## What the close-ups teach

- 🔎 **Studs are everywhere in Steal a Brainrot** — ground, carpet, walls. 🧠 Classic studs make a simple, flat-colour world look intentional and 'Roblox-y', and they hide the lack of texture detail.
- 🔎 **TFFA uses the checkerboard as a progress bar** — each biome block has its own checker colours (grass green → sand → lava red → void purple).
- 🔎 **RIVALS keeps arenas pale and quiet** — tile seams and small '+' markers give scale and depth without competing with the red targets.
- 🔎 **Wood is cartoon-warm** — Fish It's dock planks have exaggerated gaps and grain so they read at distance.
- 🔎 **Brookhaven goes realistic** — believable materials make roleplay feel like a real town.

## Our versions (original kit)

![[tex-materials-gallery.jpg]]

Related: [[Textures Hub]] · [[Art Style]] · [[Model Styles in Top Games]]
