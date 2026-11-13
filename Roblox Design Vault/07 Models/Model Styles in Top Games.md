---
tags: [models, art, reference]
---

# 🔎 Model Styles in Top Games

> [!summary]
> The top games use **five construction styles**. You can tell them apart by their "tells" (stepped edges, flat facets, smooth gradients…). Pick one per game and keep every asset in it. Images below are **crops of official store images** (© their creators), shown for study.

> [!note] Confidence legend
> 🔎 observed in official store images · 🧠 inference about how it was built (tools and workflow are not published by the developers)

## Creatures

![[ref-models-creatures.jpg]]

## Pets, collectibles & loot containers

![[ref-models-pets-items.jpg]]

## Weapons, buildings & characters

![[ref-models-weapons-buildings.jpg]]

## The five styles — how to recognise and reproduce them

| Style | Tells (how to spot it) | Seen in (🔎) | Likely built with (🧠) | Strength | Watch-out |
|---|---|---|---|---|---|
| **Voxel / brick** | Stepped edges, cube-sized pixels, flat colours | [[Throw Food For Animals]] animals & food, [[Steal a Brainrot]] units, Lucky Blocks, Steal An Egg's Yeti | MagicaVoxel / Blockbench, or Studio parts → exported to one mesh | Fast to make in volume; nostalgic Roblox look | Triangle bloat if exported per cube → [[Playbook - Voxel Creatures]] |
| **Faceted low-poly** | Flat triangular facets, few polygons, gradient lighting | [[Steal An Egg]] snake & eggs, environment props | Blender (low subdivision + flat shading) | Reads 'premium' while staying cheap | Too few facets looks unfinished on hero models |
| **Smooth stylised** | Soft shading, curves, glowing details | Steal An Egg icon creatures, TFFA phoenix & dragon, [[Fish It]] sea monsters | Blender sculpt → retopo → bake textures | Most impressive reveals / bosses | Expensive to produce; needs good textures |
| **Soft vinyl toy / cube-body** | Rounded cube or bean bodies, huge eyes, pastel colours | [[Adopt Me]] pets, [[Pet Simulator 99]] cube pets | One body template + parts in Blender | Lovable; thousands of variants from one template | Variants blur together without strong silhouettes |
| **Flat-contrast / toy weapons** | Chunky, rounded weapons; plain characters; pale arenas | [[RIVALS]] weapons and arenas | Blender hard-surface with bevels | Readability in fast combat; skins pop | Needs a strict palette or it looks like a toy box |
| *(plus)* **Clean realism** | Real proportions, neutral materials | [[Brookhaven RP]] houses & cars | Blender + PBR (SurfaceAppearance) | Believable roleplay stage | Heavier assets; colour comes from avatars |
| *(plus)* **Painted 2D key art** | Illustrated, brush texture | [[Forsaken]], [[Blox Fruits]] store art | Illustration (not models) | Sells characters and lore | Store art must still match in-game models |

## What the official close-ups teach

- 🔎 **Creatures are posed to threaten or to be stolen**: open mouths, '!!' alarm, raised claws — model faces and mouths need enough geometry to read at thumbnail size.
- 🔎 **Containers are designed like collectibles**: Steal An Egg's spiked T-Rex egg, Brainrot's winged Lucky Block, Fish It's gacha items — the container *previews* the reward.
- 🔎 **Recolour variants are everywhere**: Brainrot's pink 'Candy' dragon, TFFA's rainbow gorilla, golden/rainbow pets → [[Playbook - Cube Pets & Variants]].
- 🔎 **Weapons are oversized and simple**: RIVALS' guns have big, readable shapes with one accent colour → [[Playbook - Weapons & Tools]].
- 🔎 **Buildings are boxes**: Brainrot bases are stacked red slabs with a sign; Brookhaven houses are clean blocks with glass → [[Playbook - Bases & Props from Parts]].

## Original examples in each style (made for this vault)

| Style | Example | Page |
|---|---|---|
| Voxel | Voxel dino 'Chompy' | ![[model-voxel-dino-sheet.jpg]] |
| Faceted low-poly | Biome eggs, environment kit | ![[model-eggs.jpg]] |
| Cube-body pet | 'Cubby' cube pet | ![[model-cube-pet-variants.jpg]] |
| Toy weapon | Toy blaster | ![[model-toy-blaster.jpg]] |
| Part-built building | Steal-tycoon base | ![[model-base-parts.jpg]] |

Related: [[Art Style]] · [[Color Palettes]] · [[Models Hub]]
