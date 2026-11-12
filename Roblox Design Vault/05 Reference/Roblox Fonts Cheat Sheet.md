---
tags: [reference, typography]
---

# Roblox Fonts Cheat Sheet

Rendered specimens (same open-source font files Roblox ships): ![[gui-font-specimens.png]]

| `Enum.Font` | Family | Personality | Use for | Avoid for |
|---|---|---|---|---|
| `FredokaOne` | Fredoka One | round, heavy, friendly | simulator numbers, buttons, billboards | long text |
| `LuckiestGuy` | Luckiest Guy | cartoon, all-caps, bold | window titles, reveal text, logos | body text |
| `Bangers` | Bangers | comic, condensed, punchy | event banners, "ADMIN ABUSE!" | small sizes |
| `GothamBlack` / `GothamBold` / `GothamMedium` | Gotham → Montserrat | geometric, clean | FPS HUD, menus, modern UI | cartoon titles |
| `Montserrat` | Montserrat | geometric | same as Gotham | — |
| `BuilderSans` (via `Font.new("rbxasset://fonts/families/BuilderSans.json")`) | Builder Sans | Roblox's own UI face | body, settings, descriptions | flashy titles |
| `SourceSans` / `SourceSansBold` | Source Sans | neutral (legacy default) | body text | headings |
| `Nunito` | Nunito | rounded, soft | friendly body text | — |
| `DenkOne` | Denk One | chunky, sporty | stat labels | body |
| `TitilliumWeb` | Titillium Web | tech | sci-fi menus | cute games |
| `Oswald` | Oswald | tall, condensed | scoreboards, ammo | long text |
| `Arcade` | Press Start 2P | pixel | retro games | anything else |
| `Creepster` | Creepster | dripping horror | horror titles only | numbers, body |
| `SpecialElite` | Special Elite | typewriter | horror notes, lore | HUD numbers |
| `GrenzeGotisch` | Grenze Gotisch | blackletter | dark fantasy headings | small text |
| `PermanentMarker` | Permanent Marker | handwritten | signs, stickers | body |
| `PatrickHand` / `Kalam` | Patrick Hand / Kalam | handwritten | notes, kid-friendly | headings |
| `Michroma` | Michroma | wide, futuristic | logos, race games | body |

## Setting fonts in code

```lua
label.FontFace = Font.fromEnum(Enum.Font.FredokaOne)
label.FontFace = Font.new("rbxasset://fonts/families/GothamSSm.json", Enum.FontWeight.Black)
label.FontFace = Font.new("rbxasset://fonts/families/BuilderSans.json", Enum.FontWeight.Bold)
```

## Outline recipe (UIStroke on text)

```lua
local stroke = Instance.new("UIStroke")
stroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Contextual -- outlines the text glyphs
stroke.Thickness = 2.5
stroke.Color = Color3.fromHex("0d1017")
stroke.LineJoinMode = Enum.LineJoinMode.Round
stroke.Parent = label
```

## Rarity gradient on text (UIGradient)

```lua
local g = Instance.new("UIGradient")
g.Rotation = 90
g.Color = ColorSequence.new(Color3.fromHex("ffe66b"), Color3.fromHex("ff8a1f")) -- Legendary
g.Parent = label -- the label's TextColor3 should be white so the gradient shows true
```

Related: [[Fonts & Typography]] · [[GUI & Menus]]
