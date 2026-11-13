---
tags: [playbook, models, weapons]
---

# 🛠️ Playbook — Weapons & Tools

> [!summary] Goal
> Weapons and tools in the style of [[RIVALS]] (and the bats, rods and pickaxes of simulators): **chunky, rounded, readable in first person on a phone**, with skins that are colour/texture swaps of one mesh. Worked example: the toy blaster (original, 1,920 tris, 11 parts, in the [[Starter Model Kit]]).

![[model-toy-blaster.jpg]]

## Official references

![[ref-models-weapons-buildings.jpg]]

🔎 RIVALS' rifles, sniper and SMG are oversized with simple blocks of colour; skins (gold SMG, blue karambit) change colour and material, not shape. ✅ Its game passes bundle **weapon + exclusive skin + charm**.

## Step 1 — Proportions for first person

1. Model from the **first-person camera** view first; that's where players see it 95% of the time.
2. Exaggerate: thick barrels, big sights, chunky grips. Thin real-world details disappear on a phone.
3. Keep the silhouette distinct per weapon class (rifle, sniper, shotgun, melee) — test with [[model-silhouette-test.jpg|the silhouette test]].

## Step 2 — Build (Blender)

- Primitive-based hard surface: boxes and cylinders with **small bevels (2 segments)** where light catches.
- Cylinders 12–16 sides; hidden faces removed; total 1,000–5,000 tris ([[Model Budgets & Specs]]).
- Separate **skinnable regions**: main body, accent parts, dark parts — each region maps to one colour/texture slot.
- Origin at the **grip**.

## Step 3 — Tool setup in Studio

1. Create a `Tool`; the main part must be named **`Handle`** (when `RequiresHandle` is true).
2. Weld the other parts to the Handle (`WeldConstraint`s), all unanchored, `CanCollide` off, `Massless` on.
3. Adjust `Tool.Grip` so the hand holds the grip (test in Play mode; the hand uses the right-grip attachment).
4. For FPS games 🧠 most use a separate **viewmodel** (arms + weapon parented to the camera on the client) and the third-person tool for everyone else.

## Step 4 — Skins

| Skin type | Change | Cost |
|---|---|---|
| Colour skin | part `Color`s / palette swap | free to make — great for common skins |
| Material skin | `Material`/`SurfaceAppearance` (metal, neon, glass) | cheap |
| Pattern skin | new texture (camo, candy stripes) | one texture per skin |
| Mesh skin | new mesh for the same weapon | expensive — keep for top-tier skins |
| Charms | small hanging model attached to every weapon | ✅ RIVALS sells cross-weapon charms |

Store skins as data: `{weaponId, skinId, colors | textureId | meshId}`, apply on equip.

## Step 5 — Feedback models

- Muzzle flash (`ParticleEmitter` + short `PointLight`), tracer (`Beam`), shell casings (pooled), hit sparks.
- Melee: weapon trail (`Trail` between two attachments on the blade).

## Checklist

- [ ] Reads in first person on a phone; distinct silhouettes per class.
- [ ] Origin at the grip; `Handle` named and welded.
- [ ] Skinnable regions separated; at least two skins tested.
- [ ] Effects pooled; triangle budget respected.
