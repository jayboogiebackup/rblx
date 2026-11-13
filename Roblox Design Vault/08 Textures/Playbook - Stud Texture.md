---
tags: [playbook, textures, studs, luau]
---

# 🛠️ Playbook — Stud Texture

> [!summary] Goal
> The classic Roblox stud look (🔎 all over [[Steal a Brainrot]]) in a modern, performant way. Four methods, cheapest to most expensive. The [[Texture Kit]] includes everything you need: `studs_OVERLAY.png`, `studs_ALB/NOR/RGH.png`, `studs_BAKED.png` and `inlets_OVERLAY/NOR.png`.

![[tex-studs-methods.jpg]]

## Which method?

| Method | Looks | Cost | Colour | Use when |
|---|---|---|---|---|
| 1. Legacy `SurfaceType.Studs` | authentic old studs | free | Part.Color | quick tests, retro remakes (deprecated) |
| 2. **Texture overlay** | studs with baked light | very cheap | Part.Color shows through | top faces of floors, plates, bricks |
| 3. **MaterialVariant** | studs that react to light on every face | cheap | Part.Color tints the map | whole maps, all faces, recolourable bricks |
| 4. Real geometry | true 3D studs | expensive (64 tris per stud) | any | close-up hero objects only |

## Method 1 — Legacy surface (quick test)

The Surface tool was removed and the API is deprecated, but the property still works when set from a script (DevForum):

```lua
-- Command Bar: studs on top, inlets underneath, for every selected part
for _, part in game:GetService("Selection"):Get() do
	if part:IsA("BasePart") then
		part.TopSurface = Enum.SurfaceType.Studs
		part.BottomSurface = Enum.SurfaceType.Inlet
	end
end
```

Don't build a game on this — use Method 2 or 3.

## Method 2 — Texture overlay (any part colour)

1. Upload `studs_OVERLAY.png` (Asset Manager → Import). It's transparent except for the highlights and shadows, so the **part's own colour shows through**.
2. Add a `Texture` to the part: `Texture = rbxassetid://<id>`, `Face = Top`, **`StudsPerTileU = 2`, `StudsPerTileV = 2`** (the image holds 2 × 2 studs).
3. Keep parts on **whole-stud sizes and positions** so studs line up between neighbouring parts.

Automate it with a tag:

```lua
-- ServerScriptService/StudOverlay.server.lua
local CollectionService = game:GetService("CollectionService")

local STUD_OVERLAY = "rbxassetid://0" -- your uploaded studs_OVERLAY.png
local FACES = { Enum.NormalId.Top } -- add Front/Back/Left/Right for the full classic look

local function addStuds(part: Instance)
	if not part:IsA("BasePart") then return end
	for _, face in FACES do
		local t = Instance.new("Texture")
		t.Name = "Studs_" .. face.Name
		t.Texture = STUD_OVERLAY
		t.Face = face
		t.StudsPerTileU = 2
		t.StudsPerTileV = 2
		t.Parent = part
	end
end

for _, part in CollectionService:GetTagged("Studded") do addStuds(part) end
CollectionService:GetInstanceAddedSignal("Studded"):Connect(addStuds)
```

Use `inlets_OVERLAY.png` on `Bottom` faces for the classic underside.

## Method 3 — MaterialVariant (studs that react to light)

1. Upload `studs_ALB.png`, `studs_NOR.png`, `studs_RGH.png`.
2. Create the variant (Material Manager, or run once in the Command Bar):

```lua
local MaterialService = game:GetService("MaterialService")

local v = Instance.new("MaterialVariant")
v.Name = "ClassicStuds"
v.BaseMaterial = Enum.Material.Plastic
v.ColorMap = "rbxassetid://0"     -- studs_ALB.png (light grey → tinted by Part.Color)
v.NormalMap = "rbxassetid://0"    -- studs_NOR.png (OpenGL)
v.RoughnessMap = "rbxassetid://0" -- studs_RGH.png
v.StudsPerTile = 2                -- image holds 2 × 2 studs
v.Parent = MaterialService
```

3. Apply it:
   - **Per part**: `part.Material = Enum.Material.Plastic` and `part.MaterialVariant = "ClassicStuds"`.
   - **Everywhere**: `MaterialService:SetBaseMaterialOverride(Enum.Material.Plastic, "ClassicStuds")` — every Plastic part in the game becomes studded.
4. Colour with `Part.Color` — one variant serves every brick colour.

![[tex-tiling.jpg]]

> [!warning] MaterialVariants apply to every face
> Walls and undersides get studs too (that's the 🔎 Brainrot look). For studs on top faces only, use Method 2.

## Method 4 — Real geometry

Only for close-up hero objects (a giant LEGO-style trophy, a menu background). 16 studs on a 4 × 4 brick add 1,024 triangles (see the image above) — multiply by a whole map and phones suffer.

## Make your own stud texture (Krita / GIMP / Photoshop)

1. **Canvas 512 × 512**, grid 2 × 2 (256 px per stud cell).
2. **Height map**: black background; white circles centred in each cell, radius ≈ 30% of the cell (77 px), with a 6–10 px soft edge.
3. **Normal map**: Krita *Filter → Edge Detection → Height to Normal Map* or GIMP *Filters → Generic → Normal Map*; make sure it's **OpenGL** (green = up — flip the green channel if your tool outputs DirectX).
4. **Colour map**: flat light grey (≈ #DBDBDB) so `Part.Color` can tint it.
5. **Roughness**: mid grey (≈ 0.55), stud tops slightly smoother.
6. **Overlay version**: on a transparent layer paint a soft white highlight on the upper-left of each stud and a dark shadow on the lower-right + a soft drop shadow; keep alpha ≤ 60%.
7. **Check tiling**: offset by half (GIMP *Layer → Transform → Offset*, Krita wrap-around mode) — no seams.
8. Export PNG; upload; set StudsPerTile = studs in the image.

## Troubleshooting

| Problem | Fix |
|---|---|
| Studs don't line up between parts | Use whole-stud part sizes and positions; adjust `OffsetStudsU/V` by 0.5 if needed |
| Shimmering / moiré at distance | Lower overlay contrast; don't use StudsPerTile 1 with a 2 × 2 image |
| Studs look flat | Light is straight overhead — angle the sun (`Lighting.ClockTime`, `GeographicLatitude`) |
| Colour looks washed out | Colour map too bright/dark — keep it light grey, tint with `Part.Color` |
