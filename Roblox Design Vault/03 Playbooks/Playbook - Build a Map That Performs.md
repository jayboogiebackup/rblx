---
tags: [playbook, map, performance]
---

# 🛠️ Playbook — Build a Map That Performs

> [!summary] Goal
> A progression map (zones that get harder, prettier and more valuable) that reads instantly, stays clear where the gameplay happens, and runs on a cheap phone. Design reasoning: [[Maps & World Building]] · Style: [[Art Style]]

![[throw-food-for-animals_thumb-1.jpg]]

## Step 1 — Paper plan (30 minutes, saves weeks)

| Zone | Gate (stat / price) | Dominant hue | Props | New collectible tier | Music |
|---|---|---|---|---|---|
| 1 Meadow | free | grass green | trees, fences | Common–Rare | calm |
| 2 Desert | Speed 500 | sand yellow | cacti, bones | up to Epic | percussion |
| 3 Tundra | Speed 1,500 | ice white/blue | ice spikes | up to Legendary | chimes |
| 4 Volcano | Speed 4,000 | lava red/black | obsidian | up to Mythic | drums |
| 5 Void | Speed 10,000 | neon purple | floating grid | Secret | synth |

## Step 2 — Block-out in Studio

1. **Greybox** each zone with plain parts; walk it with the real character speed.
2. **Mark the gameplay lanes** (carry path / throw lane / duel sightlines) and keep them prop-free.
3. **Gate each zone visibly**: coloured border wall or ring + `BillboardGui` sign with the requirement ("🔒 Need 1,500 Speed").
4. Put **spawn, shop, upgrades and pens/bases within ~10 s of walking** of each other.

## Step 3 — Dress it (style rules)

- One dominant hue per zone (see [[Color Palettes]]); one accent for loot (gold or purple).
- Surface language from the [[Texture Kit]]: checker grass per zone, studs on plates and bricks ([[Playbook - Custom Materials with MaterialService]]).
- Hero props near spawns/goals; cheap filler toward edges; fog/atmosphere hides the edge of the world.
- Signposts and landmarks every ~100 studs in hubs.

## Step 4 — Performance settings

| Setting | Value | Why |
|---|---|---|
| `Workspace.StreamingEnabled` | `true` | Only nearby parts load on phones. |
| `Workspace.StreamingTargetRadius` | tune (e.g. 512–1024) | Larger for open throw lanes, smaller for dense towns. |
| `Model.ModelStreamingMode` | `Atomic` for pens/bases, `Persistent` only for things scripts need everywhere | Avoid half-loaded models. |
| Decorative parts | `Anchored`, `CanCollide=false`, `CanTouch=false`, `CanQuery=false` | Removes physics/raycast cost. |
| MeshParts | reuse the same mesh; `CollisionFidelity=Box` for props; `RenderFidelity=Automatic` | Memory + physics savings. |
| Small detail | Textures/Decals instead of geometry | Fewer triangles. |
| Lighting | `Technology = ShadowMap` or `Future`, one `Atmosphere`, limited shadow-casting lights | Looks good, stays cheap. |
| Unanchored parts | as few as possible | Physics is the #1 phone killer. |

## Step 5 — Test like a player

- [ ] **Device Emulator** + a real **low-end Android phone**.
- [ ] Open **Developer Console (F9)** → Memory; **MicroProfiler** (Ctrl+F6) for frame spikes.
- [ ] Walk every zone with 5–8 players' worth of pets/bases on screen (worst case).
- [ ] First zone visible and playable within **5 seconds** of joining.

## Step 6 — Ship zones as updates

A new zone (+ its collectibles + a title tag `[🌋 NEW ZONE]`) is the cheapest 'big update' — 📰 [[Throw Food For Animals]] shipped a new map ~7 weeks after launch.
