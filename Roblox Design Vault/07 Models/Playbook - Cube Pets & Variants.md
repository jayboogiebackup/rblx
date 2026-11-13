---
tags: [playbook, models, pets]
---

# 🛠️ Playbook — Cube Pets & Variants

> [!summary] Goal
> One pet **template** that becomes hundreds of sellable pets: recolours, golden/rainbow/neon variants, sizes and rarity effects — the approach behind [[Pet Simulator 99]]'s ✅ "3,000+ pets" and the golden/rainbow/huge variants it sells passes for. Worked example: 'Cubby' (original, 1,800 tris, in the [[Starter Model Kit]]).

![[model-cube-pet-variants.jpg]]

## Official references

![[ref-models-pets-items.jpg]]

🔎 Pet Simulator 99's pets share a rounded cube body with huge eyes; Adopt Me's pets are soft 'vinyl toys'; both rely on face + ears + colour for identity.

## Step 1 — Build the template (Blender or Blockbench)

| Part | Shape | Triangles (Cubby) | Notes |
|---|---|--:|---|
| Body | rounded cube (bevel ≈ 20% of size) | 588 | the face lives on the front of the body |
| Ears ×2 + inner ears ×2 | 4-sided pyramids | 32 | swap these per species (cat, bunny, dragon horns) |
| Eyes ×2 + shines ×2 | squashed spheres | 408 | biggest identity feature — make them huge |
| Cheeks ×2, nose | flattened spheres | 196 | colour accents |
| Feet ×4 | small rounded boxes | 432 | walk cycle |
| Tail | half torus | 144 | swap per species |

![[model-cube-pet-anatomy.jpg]]

Keep parts **separate** (one Model, many MeshParts or one skinned mesh): swapping ears, tails, eyes or adding accessories (hats, wings) creates new species without touching the body.

## Step 2 — Variant system (same mesh, new look)

| Variant | Change | In Studio |
|---|---|---|
| Recolour / species | body + ear colours | `Color` or a new palette/`TextureID` |
| **Golden** | metal material | `SurfaceAppearance` with high metalness, or `Material = Foil/Metal` + gold `Color` |
| **Rainbow** | gradient colours | gradient texture (animate by swapping or scrolling textures) |
| **Neon / shiny** | glow | `Material = Neon` on accents, `PointLight`, sparkle `ParticleEmitter` |
| **Huge** | size | scale the model (`Model:ScaleTo(2.6)`) — keep the same mesh |

> [!tip] Sizes as a stat
> ✅ Steal An Egg sells "sizes" and 📰 heavier eggs hatch higher-income pets. Store `Size` as an attribute and scale with `Model:ScaleTo(size)` so one asset covers the whole range.

## Step 3 — Rarity shell

![[model-rarity-shell.jpg]]

Layer rarity **around** the pet (re-usable on any pet):
1. **Outline shell** — a copy of the body with inverted normals (back faces), scaled ~1.1, in the rarity colour; or a `Highlight` for the very rarest (Highlights are limited on screen).
2. **Light** — a `PointLight` in the rarity colour for Legendary+.
3. **Particles** — sparkles; count scales with rarity (Common 0 → Secret lots).
4. **Colour** — rainbow body for Secret/OG.

## Step 4 — Follow behaviour & performance

- 🧠 Pets that follow players are usually **client-side visuals**: the server stores which pets you own; each client positions them (lerp `PivotTo` toward a slot behind the player) — no physics, no network traffic per frame.
- Set `CanCollide`, `CanTouch`, `CanQuery` off; `CastShadow` off for small pets.
- Reuse the same mesh for all copies; vary only colour/texture.

## Step 5 — Animate

Bounce (Root → Body), ear wiggle, tail wag, foot shuffle — 11 bones on Cubby ([[Playbook - Rigging & Animating Models]]). A procedural bob (see [[Playbook - Juice & Animation Recipes#7. Idle bob for pets/eggs]]) is enough for followers.

## Checklist

- [ ] Template under ~2,000 tris; eyes readable at 64 px.
- [ ] Ears/tail/eyes swappable.
- [ ] Golden, rainbow, neon and huge variants tested side by side.
- [ ] Rarity shell works on every species.
- [ ] 20+ pets on screen hold frame rate on a phone.
