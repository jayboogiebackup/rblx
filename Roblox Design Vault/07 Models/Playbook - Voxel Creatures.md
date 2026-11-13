---
tags: [playbook, models, voxel]
---

# 🛠️ Playbook — Voxel Creatures

> [!summary] Goal
> Build a voxel creature in the style of [[Throw Food For Animals]] animals and [[Steal a Brainrot]] units: chunky, readable, one tiny palette texture, and **greedy-meshed** so 1,190 voxels ship as ~1,264 triangles instead of 14,280. Worked example: 'Chompy' the voxel dino (original, in the [[Starter Model Kit]]).

![[model-voxel-dino-sheet.jpg]]

## Official references

![[ref-models-creatures.jpg]]

🔎 TFFA's T-Rex, rainbow gorilla and voxel foods, Brainrot's candy dragon and Lucky Blocks, and Steal An Egg's Yeti are all built from visible cubes.

## Step 1 — Pick a grid size

| Grid (longest side) | Look | Use for |
|---|---|---|
| 8–16 voxels | very chunky, iconic | food, small props, eggs |
| 16–32 voxels | readable face + limbs | pets, common creatures (Chompy is 11 × 19 × 31) |
| 32–64 voxels | detailed | bosses, hero creatures |

Rule: **eyes at least 2 × 2 voxels**, mouth at least 1 voxel tall, the outline of the silhouette must survive the grid.

## Step 2 — Model in a voxel tool

**MagicaVoxel** (free) or **Blockbench** (free, voxel-style boxes):
1. Block in the big volumes: body, head, legs, tail.
2. Carve the silhouette (side view first — that's what players see when the creature walks).
3. Add the face last: eyes, mouth, teeth, cheeks.
4. Limit the palette to **≤ 16 colours** (Chompy uses 8: body, stripes, belly, spikes, white, black, mouth, feet).
5. Add **one accent** (Chompy's orange spikes) — it's what people remember.

> [!tip] Built with Studio parts?
> Many Roblox voxel models start as Studio parts. When it's final: select it → **Export Selection** (OBJ) → clean up in Blender → re-import as **one MeshPart**. Hundreds of parts → one mesh = far cheaper.

## Step 3 — Export without triangle bloat

![[model-voxel-meshing.jpg]]

| Export | Chompy's triangles | When |
|---|--:|---|
| Every cube | 14,280 | never ship this |
| Hidden faces removed | 2,540 | acceptable |
| **Greedy-merged** | **1,264** | ship this |

How to get the greedy result:
- MagicaVoxel's OBJ export already removes hidden faces; for further merging use Blender **Limited Dissolve** with *Delimit: UVs* (merges coplanar faces of the same colour) then triangulate.
- Or write your own greedy mesher (this vault's renderer uses the classic greedy-meshing algorithm).

## Step 4 — Palette texture

1. Use a **square** palette (e.g. 4 × 4 cells of 16 px = 64 × 64), not a 256 × 1 strip — 📰 DevForum users report colour shifts with strip palettes.
2. Every face's UVs point at the **centre** of its colour cell (so filtering never bleeds into the neighbour).
3. In Studio set the texture as `MeshPart.TextureID` (or a SurfaceAppearance `ColorMap`).
4. **Variants = palette swaps**: Golden, Candy, Halloween… same mesh, different 64 × 64 image.

## Step 5 — Make it alive

- Voxel creatures don't need a skinned mesh: split into **body, head/jaw, tail, legs** as separate MeshParts joined by `Motor6D`s and animate those ([[Playbook - Rigging & Animating Models]]).
- Idle: 2-voxel head bob + tail sway. Walk: leg swing ±25°. Eat: jaw open + chomp sound.

![[model-rigs.jpg]]

## Checklist

- [ ] Reads as a silhouette at 64 px.
- [ ] ≤ 16 colours, one accent colour.
- [ ] Greedy-merged; triangles within [[Model Budgets & Specs|budget]].
- [ ] Square palette texture; recolour variants tested.
- [ ] Pivot at the feet; real scale vs avatar.
