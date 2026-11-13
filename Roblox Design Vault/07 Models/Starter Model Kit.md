---
tags: [models, starter-kit]
---

# 📦 Starter Model Kit

> [!summary]
> Five original example models (made for this vault, free to use and modify) as **OBJ files** in `99 Assets/Models/Starter Kit/`. Import them into Studio to study the topology, triangle budgets and part splits from the playbooks — then replace them with your own art.

| File | Model | Triangles | Parts | Playbook |
|---|---|--:|--:|---|
| `voxel-dino.obj` + `.mtl` + `voxel-dino_palette.png` | 'Chompy' voxel dino (greedy-meshed, palette UVs) | 1,264 | 1 | [[Playbook - Voxel Creatures]] |
| `cube-pet.obj` | 'Cubby' cube pet template | 1,800 | 17 | [[Playbook - Cube Pets & Variants]] |
| `faceted-egg.obj` | Faceted egg (180-triangle icosphere) | 180 | 1 | [[Playbook - Eggs & Loot Containers]] |
| `toy-blaster.obj` | Toy blaster | 1,920 | 11 | [[Playbook - Weapons & Tools]] |
| `low-poly-props.obj` | Round tree, pine, rock | 166 | 8 | [[Playbook - Bases & Props from Parts]] |

All files are in **studs** (1 OBJ unit = 1 stud) with the origin at the model's feet/base.

![[model-voxel-dino-sheet.jpg]]

## Import into Roblox Studio

1. Open a place → **Import 3D** (File menu or the Home/Avatar tab) → pick the `.obj`.
2. In the importer preview, check the **scale** (the dino should be ≈ 2.8 × 4.8 × 7.8 studs) and that the model sits on the ground.
3. Import. Multi-part files (pet, blaster, props) arrive as a **Model** with one MeshPart per part.
4. **Dino texture:** if the palette doesn't come through automatically, upload `voxel-dino_palette.png` (Asset Manager → Import) and set it as the dino MeshPart's `TextureID`.
5. **Pet / blaster / props colours:** these files carry geometry only — colour each MeshPart (`Color`, `Material`) or apply your own textures. Use the renders as a colour guide:

![[model-cube-pet-variants.jpg]]
![[model-toy-blaster.jpg]]
![[model-env-kit.jpg]]

## Suggested exercises

1. **Recolour the dino** by editing the 64 × 32 palette PNG only (make a 'Golden' and a 'Candy' variant).
2. **Make three new pet species** from the cube pet by swapping ears and tail only.
3. **Rig the dino** with Motor6Ds: split jaw, tail and legs into separate parts ([[Playbook - Rigging & Animating Models]]).
4. **Make a 'void' egg**: duplicate the egg, colour it dark, add a `PointLight` and sparkles ([[model-eggs.jpg]]).
5. **Give the blaster a Tool setup**: rename the receiver to `Handle`, weld the rest, set the grip.

> [!note] Where these came from
> The models were generated procedurally for this vault and rendered with three.js. They're simple on purpose — teaching assets, not production art.
