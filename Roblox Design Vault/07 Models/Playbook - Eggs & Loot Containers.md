---
tags: [playbook, models, eggs]
---

# 🛠️ Playbook — Eggs & Loot Containers

> [!summary] Goal
> Eggs, crates and lucky blocks are **the loot box you can see before you open it**. In [[Steal An Egg]] they *are* the gameplay object you steal. Make them readable by biome/rarity at a glance, cheap enough to place dozens, and ready to crack open in the reveal. Worked example: four faceted biome eggs from one 180-triangle mesh (in the [[Starter Model Kit]]).

![[model-eggs.jpg]]

## Official references

🔎 Steal An Egg: spiked T-Rex egg, rainbow snowflake egg, cosmic egg; Steal a Brainrot: winged skull Lucky Block; TFFA: voxel foods as 'ammo' — see [[ref-models-pets-items.jpg]].

## Step 1 — Base mesh (Blender)

1. *Add → Mesh → Ico Sphere* — Blender's **Subdivisions 2 = 80 triangles, 3 = 320**. This vault's example sits in between at **180** (each icosahedron edge split in three — the 'detail 2' in the render).
2. Scale to an egg: X/Y 0.92, height 1.25. Optionally pull the top vertex up a little.
3. **Shade Flat** for the gem-like facets (or Shade Smooth + a painted texture for a soft egg).
4. Origin at the bottom so it sits on the ground.

## Step 2 — Biome / rarity patterns

Colour **per face** (palette UVs, like [[Playbook - Voxel Creatures#Step 4 — Palette texture]]):

| Egg | Rule | Reads as |
|---|---|---|
| Meadow | cream base + green spots | starter, common |
| Desert | sand + orange zig-zag band | warm biome |
| Tundra | white → ice-blue gradient, random lighter shards | cold biome |
| Void | near-black + magenta band + purple stars, emissive glow | late-game, rare |

Make **biome = pattern** and **rarity = effects** (glow, particles, shell) so the two systems never fight.

## Step 3 — Hero containers

For the rarest eggs, add **silhouette features**: spikes, horns, wings, crowns (🔎 Steal An Egg's T-Rex egg has dino spikes; Brainrot's Lucky Block has wings). Budget up to ~600 triangles.

## Step 4 — Crack & hatch models

1. Duplicate the egg and split it into **2–5 shell pieces** along a zig-zag line (Blender: knife tool → separate by loose parts).
2. In the reveal, swap the whole egg for the pieces and push them outward with a short tween / physics impulse.
3. Pair with the [[gui-hatch-sequence.jpg|4-beat hatch sequence]] and [[Playbook - Egg Hatch & Pet System]].

## Step 5 — In the world

- Idle: slow bob + rotate (procedural, no rig).
- Pen timers: BillboardGui above the egg (⏳ countdown) — see [[gui-world-space-kit.png]].
- Rarity glow: `PointLight` + sparkles for Legendary+; `Highlight` only for the very rarest.
- Carry state: weld above the head (🔎 the Steal An Egg thumbnails show eggs held overhead) — [[Playbook - Steal-a-X Base Loop]].

## Checklist

- [ ] Biome readable from pattern alone; rarity from effects alone.
- [ ] ≤ 600 tris; one shared palette across all eggs.
- [ ] Crack pieces ready for the reveal.
- [ ] Looks great held overhead and sitting in a pen.
