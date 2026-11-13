---
tags: [playbook, models, pipeline]
---

# 🛠️ Playbook — Model Creation Pipeline

> [!summary] Goal
> Take any model — pet, creature, egg, weapon, building or prop — from idea to a performant asset in a live Roblox game. The nine steps match the diagram. Limits and budgets: [[Model Budgets & Specs]].

![[diagram-model-pipeline.jpg]]

## Tools (all have free options)

| Tool | Best for | Free? |
|---|---|---|
| **Blender** | Everything: low-poly, sculpt, UVs, rigging, animation, FBX export | ✅ |
| **Blockbench** | Low-poly / blocky / voxel-style models, quick texturing | ✅ |
| **MagicaVoxel** | True voxel models; exports OBJ + palette PNG | ✅ |
| **Roblox Studio** | Part-built models, final setup, Animation Editor, testing | ✅ |
| Substance Painter / Aseprite / Krita | Textures (PBR or hand-painted) | paid / ✅ / ✅ |

## Step 1 — Reference

1. Make a mood board from [[Model Styles in Top Games]] (crops of what the top games actually ship).
2. Draw the **silhouette** (black shape) first. If it isn't recognisable, nothing else will save it.
3. Decide the **size in studs** next to a ≈5-stud avatar, and the **budget** from the table in [[Model Budgets & Specs]].
4. Fill in a [[Template - Model Spec]].

## Step 2 — Blockout

1. Big primitive shapes only (cubes, spheres, cylinders). No detail.
2. Import into Studio **at real scale** and look at it through the actual game camera on a phone-sized viewport.
3. Iterate proportions here — it's 10× cheaper than after texturing. Exaggerate heads, eyes and the hero feature.

## Step 3 — Model

1. Build over the blockout. Keep edge loops where it will bend (necks, tails, legs).
2. **Delete hidden faces** (inside joins, undersides that never show).
3. Check the triangle count (Blender: *Overlays → Statistics*). Hit the budget **before** texturing.
4. Set the **origin/pivot**: feet centre for creatures, grip for tools, base centre for buildings.
5. Apply all transforms (*Object → Apply → All Transforms*) before export.

![[model-cube-pet-anatomy.jpg]]

## Step 4 — UV + texture

Choose one approach per game:

| Approach | Look | How |
|---|---|---|
| **Palette texture** | Flat-colour stylised (voxel, low-poly) | Tiny image of colour squares; every face's UVs are scaled down into its colour square. One texture for a whole family of models. |
| **Atlas** | Hand-painted, patterned | Several models share one 512–1024 texture. |
| **PBR (SurfaceAppearance)** | Realistic / premium | ColorMap + NormalMap (OpenGL) + Roughness + Metalness, ≤ 1024². |
| **Vertex colours** | Quick prototyping | Bake to a texture before shipping so every pipeline step supports it. |

![[model-voxel-dino-sheet.jpg]]

More on texture objects, tiling and PBR sets: [[Textures Hub]] · [[Texture Objects & Specs]].

## Step 5 — Rig + animate (skip for static models)

See [[Playbook - Rigging & Animating Models]]. Keep bones few; name them clearly (`Root`, `Body`, `Head`, `Tail1`…).

## Step 6 — Export

**Blender → FBX** (rigged or static):
- *Selected Objects* only · *Apply Scalings: FBX Unit Scale* · scale ≈ 0.01 so 1 m = 1 stud (calibrate!)
- *Armature: Add Leaf Bones* **off** · *Bake Animation* on if exporting animation
- Forward / Up: leave Blender defaults unless your calibration shows a rotation

**OBJ** (static): include `.mtl` + texture next to it. **GLB**: bundles textures in one file (where your Studio supports it).

## Step 7 — Import

1. Studio → **Import 3D** (3D Importer). Pick the file.
2. Check the preview: **scale**, **origin**, **rig** detected, **texture** found.
3. Keep each mesh under ≈20k triangles (split big models).
4. Import as a **Model**; rename parts sensibly.

## Step 8 — Set up in Studio

- `PrimaryPart` = the root/body part; `Anchored` as needed.
- `CollisionFidelity = Box` (pets/props) or `Hull`; `RenderFidelity = Automatic`.
- Turn off `CanCollide/CanTouch/CanQuery/CastShadow` where not needed.
- Add **Attributes** (`Rarity`, `Income`, `Variant`) and **CollectionService tags**.
- Save as a **Package** if the model is reused (every copy updates when you publish a change).

## Step 9 — Test on a phone

- [ ] Silhouette at 64 px ([[model-silhouette-test.jpg]]).
- [ ] 20+ copies on screen at once (pens, swarms) — check frame rate.
- [ ] Developer Console (F9) → Memory; MicroProfiler for frame spikes.
- [ ] Looks right in the store thumbnail pose and in the reveal screen.

Next: [[Playbook - Voxel Creatures]] · [[Playbook - Cube Pets & Variants]] · [[Starter Model Kit]]
