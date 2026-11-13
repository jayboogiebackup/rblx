---
tags: [models, reference, performance]
---

# 📐 Model Budgets & Specs

> [!summary]
> Roblox lets a single imported mesh go up to about **20,000 triangles** and textures up to **1024×1024** — but top games ship far less because **phones render dozens of models at once**. Budget per *model on screen*, not per file.

![[diagram-model-budgets.png]]

## Platform limits & formats

| Spec | Value | Source / confidence |
|---|---|---|
| Triangles per mesh (3D Importer) | ≈ **20,000** (≈21k quoted; older/batch paths 10k) | Roblox staff on the DevForum (📰) — split bigger models into several meshes |
| Texture size (SurfaceAppearance PBR maps) | up to **1024 × 1024** | Roblox texture specifications (docs) |
| Normal maps | **OpenGL, tangent space** | Roblox texture specifications (docs) |
| Import formats | **FBX**, **OBJ**; **glTF/GLB** (beta from 2023, used in current guides) | DevForum + guides (📰) — check your Studio's 3D Importer |
| Blender FBX export | *Apply Scalings → FBX Unit Scale*, **Add Leaf Bones OFF**, scale ≈0.01 so 1 Blender metre ≈ 1 stud | Roblox export requirements + guides (📰) — calibrate with a test cube |
| Avatar height | ≈ 5 studs (R15 default) | 🧠 block out next to a real avatar |
| Bones per rig | no limit found in docs | 🧠 keep pets 6–12, creatures 15–30 |

> [!tip] Calibration test (do this once per toolchain)
> Export a **4 × 4 × 4** cube from your tool, import it, and check it's exactly 4 studs. Fix scale in the exporter, not by resizing in Studio — scaled rigs and animations break.

## Recommended budgets (🧠 guideline for phone-first games)

| Asset class | Triangles | Texture | Bones | Example in this vault |
|---|--:|---|--:|---|
| Environment prop | 30–300 | shared palette / atlas | — | kit props 36–66 ([[model-env-kit.jpg]]) |
| Egg / crate / loot container | 80–600 | palette or 256² | 0–3 | faceted egg 180 ([[model-eggs.jpg]]) |
| Building / base | 300–3,000 (or 30–150 parts) | materials + 512² sign | — | base 41 parts / 492 ([[model-base-parts.jpg]]) |
| Common pet / collectible | 300–2,000 | palette or 256–512² | 6–12 | voxel dino 1,264 ([[model-voxel-dino-sheet.jpg]]) |
| Hero pet (Legendary+) | 1,000–5,000 | 512–1024² | 8–16 | cube pet 1,800 ([[model-cube-pet-anatomy.jpg]]) |
| First-person weapon | 1,000–5,000 | 512–1024² | 0–6 | toy blaster 1,920 ([[model-toy-blaster.jpg]]) |
| Boss / showcase creature | 3,000–12,000 | 1024² | 15–40 | — |

**Worst-case math:** a pen with 12 pets at 1,800 tris = 21,600 tris, × 7 bases in a [[Steal An Egg]]-sized server = ~150k tris just for pets. That's why simulators keep commons cheap and spend on heroes.

## Studio properties to set on every MeshPart

| Property | Recommended | Why |
|---|---|---|
| `CollisionFidelity` | `Box` for pets/props, `Hull` for walkable objects, `PreciseConvexDecomposition` only when needed | Collision geometry costs memory and physics time |
| `RenderFidelity` | `Automatic` | Lets the engine use lower detail at distance |
| `CanCollide` / `CanTouch` / `CanQuery` | off for decoration and pets that follow players | Removes physics and raycast cost |
| `CastShadow` | off for tiny props and particles-heavy pets | Shadows are expensive on phones |
| `Anchored` | on for static models | No physics simulation |
| `DoubleSided` | off unless the mesh is a single plane | Doubles rendered faces |
| `TextureID` / `SurfaceAppearance` | one shared texture per style | Batching and memory |
| Attributes | `Rarity`, `Income`, `Role`, `Variant` | Scripts read data, not names |

## Draw-call & memory tips

- **Reuse meshes**: 100 copies of the same MeshId + texture are far cheaper than 100 unique meshes.
- **Merge static clusters**: a fence line or a rock pile can be one mesh instead of 30 parts.
- **Split by visibility**: a boss's armour that's often hidden can be a separate mesh toggled off.
- **Avoid unions for detail**: CSG unions are convenient but heavy; export to a mesh when final.
- **Highlights are limited**: Roblox renders a limited number of `Highlight` outlines at once — use them for the rarest items only and fake outlines (back-face shell) for the rest.

Related: [[Playbook - Model Creation Pipeline]] · [[Playbook - Build a Map That Performs]] · [[Models Hub]]

Sources: [DevForum — Exceed 10,000 triangle limit](https://devforum.roblox.com/t/exceed-10000-triangle-limit/1760555) · [DevForum — 3D Import recap](https://devforum.roblox.com/t/3d-import-recap-apr-may-2023/2413182/16) · [DevForum — 3D Importer glTF beta](https://devforum.roblox.com/t/3d-importer-support-for-gltf-files-beta/2320761) · [Roblox docs — Texture specifications](https://create.roblox.com/docs/art/modeling/texture-specifications) · [Roblox docs — Export requirements](https://create.roblox.com/docs/art/modeling/export-requirements)
