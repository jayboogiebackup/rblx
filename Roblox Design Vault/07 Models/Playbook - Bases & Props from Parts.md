---
tags: [playbook, models, building, props]
---

# 🛠️ Playbook — Bases & Props from Parts

> [!summary] Goal
> Buildings and bases (like [[Steal a Brainrot]]'s multi-floor bases and [[Brookhaven RP]]'s houses) are **architecture, not sculpture** — build them from Studio parts on the stud grid. Environment props stay **tiny low-poly meshes**. Worked examples: a 41-part steal-tycoon base and a 5-prop kit (36–66 tris each).

![[model-base-parts.jpg]]

## Part 1 — A base from parts

### Step 1 — Grid & scale
- *Model tab → Move increment 1 stud, Rotate 15°*. Build on whole studs so copies tile.
- Plan floors at **8 studs** tall (comfortable for avatars + camera); doors ≥ 6 studs wide.

### Step 2 — Block by role
| Role | Parts (example) | Notes |
|---|--:|---|
| Structure | 10 | floors, walls, pillars, roof — one colour |
| Trim | 8 | edges and railings in a light accent |
| Glass | 2 | windows |
| **Slots** | 9 | gameplay pads where units sit — keep them separate |
| Sign | 3 | SurfaceGui with the owner's name |
| **Lock plate** | 1 | gameplay trigger |
| Stairs | 8 | access to the upper floor |

Tag gameplay parts (`CollectionService` tags `Slot`, `LockPlate`) and give every part a `Role` attribute — scripts find them without fragile names.

### Step 3 — Materials
- `SmoothPlastic` + bright colour for the simulator look; `Brick`, `Wood`, `Concrete` for texture. Custom looks via `MaterialService` → `MaterialVariant`.
- One base colour per player/team is enough identity (🔎 Brainrot bases are solid red with a name sign).

### Step 4 — Make it a Package
Group as a `Model` (PrimaryPart = floor) → **Convert to Package** → every base in every server updates when you publish a change.

### Step 5 — Performance
- 30–150 parts per base is fine; avoid hundreds of tiny decorative parts — use a mesh or a texture instead.
- CSG unions only for simple cut-outs; export complex unions to a mesh.
- Anchor everything; `CanTouch` off except gameplay triggers.

## Part 2 — Low-poly environment props

![[model-env-kit.jpg]]

| Prop | Recipe (Blender) | Tris |
|---|---|--:|
| Round tree | 6-sided cylinder trunk + two icospheres (subdiv 0) | 64 |
| Pine | 6-sided trunk + 3 stacked 7-sided cones | 66 |
| Rock | dodecahedron, squashed, jittered vertices | 36 |
| Bush | three icospheres (subdiv 0) | 60 |
| Fence | 2 posts + 2 rails (boxes) | 48 |

Rules: **flat shading**, one palette texture for the whole kit, colour variety by recolouring, never more than ~300 tris per prop. Scatter with random rotation/scale (±15%) so repeats don't show.

## Checklist

- [ ] Built on whole studs; floors ≥ 8 studs.
- [ ] Gameplay parts tagged and separate.
- [ ] Base saved as a Package.
- [ ] Props under 300 tris, flat-shaded, sharing one texture.
- [ ] Map-wide test with all bases + props on a phone ([[Playbook - Build a Map That Performs]]).
