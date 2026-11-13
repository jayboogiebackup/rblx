---
tags: [playbook, textures, materials, luau]
---

# 🛠️ Playbook — Custom Materials with MaterialService

> [!summary] Goal
> Turn a texture set (colour + normal + roughness) into a **MaterialVariant** you can put on any part — per part, or as a game-wide replacement for a built-in material. This is how you re-skin a whole map in one change.

![[tex-materials-gallery.jpg]]

## How it works

- `MaterialVariant`s live inside **MaterialService** (they don't work anywhere else).
- Each variant has a `BaseMaterial` (Plastic, Grass, Wood…), up to four maps (`ColorMap`, `NormalMap`, `RoughnessMap`, `MetalnessMap`), `StudsPerTile` and `Pattern` (`Regular` / `Organic`).
- Use it **per part** (`BasePart.MaterialVariant = "Name"` with a matching `Material`) or **globally** (`MaterialService:SetBaseMaterialOverride(Enum.Material.X, "Name")`). The variant's `BaseMaterial` must match the slot you override.
- If no matching variant is found, the built-in material is used.

## Step 1 — Upload the maps
Asset Manager → Import → select `name_ALB.png`, `name_NOR.png`, `name_RGH.png` (from the [[Texture Kit]] or your own).

## Step 2 — Create the variant (Material Manager)
1. Open **Material Manager** (Model tab).
2. Pick the base material (e.g. *Plastic* for studs, *Grass* for checker grass, *Wood* for planks, *Brick* for bricks).
3. Create a variant, name it (e.g. `CheckerGrass`), assign the three maps.
4. Set **StudsPerTile** (kit values: studs 2, checker 8, planks 8, bricks 6, tiles 8) and **Pattern**.
5. Optional: *Set as Override* to replace that base material everywhere.

## Step 2 (alt) — Create variants with code

```lua
-- Run once in the Command Bar (edit mode). Replace the 0s with your asset IDs.
local MaterialService = game:GetService("MaterialService")

local KIT = {
	{ name = "ClassicStuds",  base = Enum.Material.Plastic, spt = 2, alb = 0, nor = 0, rgh = 0 },
	{ name = "CheckerGrass",  base = Enum.Material.Grass,   spt = 8, alb = 0, nor = 0, rgh = 0 },
	{ name = "CheckerDirt",   base = Enum.Material.Ground,  spt = 8, alb = 0, nor = 0, rgh = 0 },
	{ name = "WoodPlanks",    base = Enum.Material.WoodPlanks, spt = 8, alb = 0, nor = 0, rgh = 0 },
	{ name = "KitBricks",     base = Enum.Material.Brick,   spt = 6, alb = 0, nor = 0, rgh = 0 },
	{ name = "ArenaTiles",    base = Enum.Material.SmoothPlastic, spt = 8, alb = 0, nor = 0, rgh = 0 },
}

for _, m in KIT do
	local v = Instance.new("MaterialVariant")
	v.Name = m.name
	v.BaseMaterial = m.base
	v.ColorMap = "rbxassetid://" .. m.alb
	v.NormalMap = "rbxassetid://" .. m.nor
	v.RoughnessMap = "rbxassetid://" .. m.rgh
	v.StudsPerTile = m.spt
	v.Parent = MaterialService
end
```

## Step 3 — Apply

```lua
-- Per part
part.Material = Enum.Material.Grass
part.MaterialVariant = "CheckerGrass"

-- Game-wide: every Grass part now uses the checker grass variant
game:GetService("MaterialService"):SetBaseMaterialOverride(Enum.Material.Grass, "CheckerGrass")
```

🧠 Global overrides also change Terrain that uses that material — check terrain areas after enabling one.

## Step 4 — Zone themes (the TFFA trick)

🔎 [[Throw Food For Animals]] changes checker colours per biome. Make one tintable checker variant and colour each zone's floor parts (`Part.Color`), or make one variant per zone (`CheckerSand`, `CheckerLava`, `CheckerVoid`) for different patterns.

![[tex-classic-scene.jpg]]

## Checklist

- [ ] Every variant's `BaseMaterial` matches how it's used.
- [ ] StudsPerTile matches what the image shows.
- [ ] `Organic` for natural surfaces, `Regular` for patterns.
- [ ] Tested on a phone at gameplay camera distance.
- [ ] Overrides documented (they silently change every part of that material).

Sources: [Roblox docs — MaterialVariant](https://create.roblox.com/docs/reference/engine/classes/MaterialVariant) · [Roblox docs — MaterialService](https://create.roblox.com/docs/reference/engine/classes/MaterialService) · [DevForum — Material Service beta](https://devforum.roblox.com/t/upload-custom-materials-in-the-new-material-service-beta/1583158?page=25) · [DevForum — removing obvious tiling](https://devforum.roblox.com/t/how-to-make-detailed-textures-and-remove-obvious-tiling-effect-no-code-required/3047355)
