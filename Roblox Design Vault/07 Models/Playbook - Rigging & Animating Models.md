---
tags: [playbook, models, rigging, animation, luau]
---

# 🛠️ Playbook — Rigging & Animating Models

> [!summary] Goal
> Make pets and creatures move with the fewest bones that still sell the motion. Two routes: **part rigs** (separate MeshParts joined by `Motor6D`) built in Studio, or **skinned meshes** (one mesh + bones) built in Blender. Both animate in Studio's Animation Editor.

![[model-rigs.jpg]]

## Choose a route

| | Part rig (Motor6D) | Skinned mesh (bones) |
|---|---|---|
| Built in | Studio (or any modeller) | Blender → FBX |
| Deformation | rigid pieces | smooth bending |
| Best for | voxel creatures, cube pets, mechs, toys | organic creatures, tails, soft bodies |
| Effort | low | medium |
| Example | Cubby's ears/tail/feet, Chompy's jaw/legs | a dragon with a bending neck |

## Bone budgets (🧠 guideline)

| Model | Bones | Example layout |
|---|--:|---|
| Pet follower | 6–12 | Root, Body, Ear.L/R, Tail, Foot ×4 (Cubby: 11) |
| Creature | 15–30 | Root, Hips, Spine, Neck, Head, Jaw, Tail1–3, legs, arms (Chompy: 18) |
| Boss | 30–60 | + fingers, wings, extra tail segments |

## Route A — part rig in Studio

1. Split the model into parts: `Body` (PrimaryPart), `Head`/`Jaw`, `Tail`, `LegL`, `LegR`…
2. Create `Motor6D`s: `Part0` = parent part, `Part1` = child part, `C0`/`C1` at the pivot (e.g. the hip).
3. Add an **`AnimationController`** with an **`Animator`** inside the model (non-Humanoid rigs).
4. Open **Animation Editor** (Avatar tab) → select the rig → keyframe.

```lua
-- Join a tail to a body at the tail's base (server or edit-time script)
local function joint(part0: BasePart, part1: BasePart, pivotWorld: CFrame)
	local m = Instance.new("Motor6D")
	m.Part0, m.Part1 = part0, part1
	m.C0 = part0.CFrame:ToObjectSpace(pivotWorld)
	m.C1 = part1.CFrame:ToObjectSpace(pivotWorld)
	m.Parent = part0
	return m
end
```

## Route B — skinned mesh from Blender

1. Add an **Armature**; place bones at joints (side view for spine/tail, front view for legs).
2. Name bones clearly; keep a single root bone at the feet.
3. Parent mesh to armature *with Automatic Weights*, then fix weights in Weight Paint mode (mouths and tails need care).
4. Export FBX: *Add Leaf Bones* **off**, *Apply Scalings: FBX Unit Scale* ([[Model Budgets & Specs]]).
5. Studio 3D Importer detects the rig → the model gets `Bone`s; add `AnimationController` + `Animator` if missing.
6. Animate in Studio's Animation Editor, or animate in Blender and use **Import from FBX Animation** in the Animation Editor.

## Animations every pet/creature needs

| Clip | Length | Loop | Notes |
|---|---|---|---|
| Idle | 1.5–3 s | ✔ | breathing, blink, tail sway — never fully still |
| Walk / run | 0.6–1 s | ✔ | match to speed so feet don't slide |
| Happy / pickup | 0.5 s | ✖ | squash & stretch hop — plays when collected |
| Action (eat, attack, steal) | 0.4–0.8 s | ✖ | anticipation → hit → recover |
| Hatch reveal pose | 1 s | ✖ | hero pose for the reveal camera |

## Playing animations

```lua
local animator = model:FindFirstChildWhichIsA("AnimationController"):FindFirstChildOfClass("Animator")
local idle = Instance.new("Animation")
idle.AnimationId = "rbxassetid://0" -- your uploaded animation
local track = animator:LoadAnimation(idle)
track.Looped = true
track:Play(0.2) -- 0.2 s fade-in
```

> [!tip] Cheap alternative for followers
> For dozens of follower pets, skip rigs entirely: procedural bob + tilt on the client ([[Playbook - Juice & Animation Recipes#7. Idle bob for pets/eggs]]). Use real animations for the reveal and for your own equipped pet.

## Checklist

- [ ] Bone count within budget; names consistent across the species.
- [ ] Pivot/root at the feet; no scale on the armature at export.
- [ ] Idle never fully still; walk speed matches movement.
- [ ] Animations reused across species that share a template.
