---
tags: [pillar, art]
---

# 🎨 Art Style

> [!summary]
> There is no single 'Roblox style' at the top — there are **five**, and each is chosen for a job: **production speed** (voxel), **readability** (flat contrast), **lovability** (soft toys), **mood** (dark + one light source) or **believability** (clean realism). Measured palettes are in [[Color Palettes]].

![[gui-palettes.png]]

## The five styles

| Style | Games | Look | Why it's chosen |
|---|---|---|---|
| **Voxel / brick-built** | [[Steal a Brainrot]], [[Throw Food For Animals]], [[Steal An Egg]] (partly) | Characters, food and terrain built from cubes; checkerboard 'studs' grass; glossy render | Hundreds of collectibles fast, consistent, nostalgic platform look |
| **Flat-contrast arena** | [[RIVALS]] | Pure red figures on white/lavender tiles; chunky toy weapons | Targets pop on any device; cosmetics read clearly |
| **Soft vinyl toy** | [[Adopt Me]], [[Pet Simulator 99]] | Rounded shapes, big glossy eyes, pastel-saturated | Pets you love, not fear; merch-friendly |
| **Dark + one light** | [[99 Nights in the Forest]], [[Forsaken]], [[Murder Mystery 2]] | 22–29% near-black; warm fire or blood-red accent | Fear is cheap to render; light = safety |
| **Clean realism** | [[Brookhaven RP]] | Neutral greys, modern architecture | A believable stage for roleplay |
| *(bonus)* **Painted anime key art** | [[Blox Fruits]] | Illustrated store images, dramatic VFX | Signals epic adventure in a feed of 3D renders |

## Style in the store images (proven examples)

![[anno-steal-an-egg-chase.jpg]]
![[anno-tffa-arc.jpg]]
![[anno-rivals-contrast.jpg]]
![[anno-brainrot-base.jpg]]

## Instructions — choosing and locking a style

1. **Pick by production volume.** >100 collectibles → voxel or a single body template (PS99 cube pets). <20 hero characters → painted/stylised roster (Forsaken).
2. **Pick by the core verb.** Shooting → contrast first. Collecting → cute/glossy. Surviving → darkness + light.
3. **Lock a palette of 5–7 colours** per biome or mode. Simulators: sky blue + grass green + one loot accent (gold/purple). Horror: near-black + one accent.
4. **Make rarity a colour language** that never changes (grey → green → blue → purple → gold → red → rainbow). ![[gui-rarity-ladder.png]]
5. **Silhouette test**: blacken every pet/character; if two look the same at 64 px, redesign one.
6. **Outline everything that matters** at thumbnail scale (white sticker outline in store art, dark UIStroke in UI).
7. **Spend polish on light, not polygons**: Future lighting + Atmosphere + one coloured light per scene.
8. **Write a one-page style sheet** (palette, outline rules, material list, 3 reference images) before modelling anything.

## Materials & lighting quick reference (🧠)

| Look | Materials | Lighting |
|---|---|---|
| Voxel sim | SmoothPlastic + subtle checker/stud Texture, Neon for loot glow | ShadowMap/Future, bright Ambient, saturated Atmosphere, no fog |
| Arena FPS | SmoothPlastic, pale tiles, few colours | Even, high-key, soft shadows; Bloom for tracers |
| Soft toy | SmoothPlastic with gradient textures, glossy specular | Warm key light, pastel sky |
| Horror | Wood/Grass/Slate PBR, dark | Fog/Atmosphere density high, one PointLight source, ColorCorrection desaturate |
| Realism | PBR materials (concrete, brick, glass) | Future lighting, neutral sky, realistic scale |

Related: [[Model Styles in Top Games]] · [[Models & Assets]] · [[Maps & World Building]] · [[Thumbnails & Icons]] · [[Color Palettes]]
