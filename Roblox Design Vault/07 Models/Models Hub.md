---
tags: [models, moc]
---

# 🧱 Models Hub — models & model creation

> [!abstract] What's in this section
> How the top Roblox games' **models** are built (creatures, pets, eggs, weapons, bases, props), the **technical limits** you have to respect, and **step-by-step creation playbooks** using original example models made for this vault. Every playbook has a matching **starter file** you can import into Studio ([[Starter Model Kit]]).

![[model-voxel-dino-sheet.jpg]]

## Start here

| Page | What you get |
|---|---|
| [[Model Styles in Top Games]] | Official close-ups from the top games, tagged by construction style, and what each style is good for |
| [[Model Budgets & Specs]] | Roblox limits (triangles, textures, formats, units) + recommended budgets per asset type |
| [[Playbook - Model Creation Pipeline]] | The 9-step pipeline from reference to in-game, with Blender / Blockbench / Studio settings |
| [[Playbook - Voxel Creatures]] | Build a voxel creature like Throw Food For Animals / Steal a Brainrot units; palette textures; greedy meshing |
| [[Playbook - Cube Pets & Variants]] | One pet template → golden / rainbow / neon / huge variants (Pet Simulator 99 style) |
| [[Playbook - Eggs & Loot Containers]] | Faceted eggs, biome patterns, crack/hatch models |
| [[Playbook - Rigging & Animating Models]] | Bones for pets and creatures, skinned meshes vs Motor6D, idle/walk/attack |
| [[Playbook - Weapons & Tools]] | Chunky first-person weapons (RIVALS style), grips, skins |
| [[Playbook - Bases & Props from Parts]] | Steal-tycoon bases and low-poly environment kits |
| [[Starter Model Kit]] | 5 importable OBJ models + palette texture |
| [[Template - Model Spec]] | A one-page spec to fill in before modelling |

## The pipeline at a glance

![[diagram-model-pipeline.jpg]]

## Example models made for this vault

> [!gallery]- 🧱 Original model renders (click to expand)
> ![[model-voxel-meshing.jpg]] ![[model-cube-pet-variants.jpg]] ![[model-cube-pet-anatomy.jpg]] ![[model-rarity-shell.jpg]] ![[model-eggs.jpg]] ![[model-rigs.jpg]] ![[model-toy-blaster.jpg]] ![[model-base-parts.jpg]] ![[model-env-kit.jpg]] ![[model-silhouette-test.jpg]]

## 15 rules for models in top Roblox games

1. **Silhouette first** — every collectible must read as a black shape at 64 px. ![[model-silhouette-test.jpg]]
2. **One template, many variants** — body template × colours × accessories × effects (✅ Pet Simulator 99 advertises 3,000+ pets).
3. **Rarity lives around the model** — outline shell, light, particles, colour — not in new meshes. ![[model-rarity-shell.jpg]]
4. **Size is a stat** — scale the same model (✅ Steal An Egg: "sizes"; 🔎 "Huge" pets).
5. **Pick one construction style per game** — voxel, faceted low-poly, smooth toy or flat-contrast (see [[Model Styles in Top Games]]).
6. **Stay far under the cap** — the importer allows ≈20k triangles per mesh; phone-first games ship pets at 300–2,000.
7. **Delete what nobody sees** — hidden faces, insides, undersides of floors.
8. **One small texture** — palette or atlas; recolour = texture swap.
9. **Pivot where it's used** — feet for creatures, grip for tools, base centre for buildings.
10. **Real scale** — an avatar is about 5 studs tall; block out next to one.
11. **Few bones** — pets 6–12, creatures 15–30; animate in Studio or import from Blender.
12. **Exaggerate the hero parts** — eyes, mouths, claws, muzzles; shrink the boring parts.
13. **Separate gameplay parts** — slots, lock plates, hitboxes as named parts with attributes.
14. **Reuse meshes** — identical MeshId + texture lets the engine batch many copies cheaply.
15. **Test with 20+ copies on a real phone** — pens and swarms are the worst case.

Textures for your models: [[Textures Hub]] · [[Texture Kit]]

Related pillars: [[Models & Assets]] · [[Pets & Collectibles]] · [[Art Style]] · [[Animation & Game Feel]]
