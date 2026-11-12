---
tags: [pillar, typography, ui]
---

# 🔤 Fonts & Typography

> [!summary]
> Simulators use **heavy rounded display fonts with a thick dark outline**, gradients for rarity and green for money. Competitive games use **geometric sans numerals** on dark plates. Horror games use **distressed/typewriter faces** sparingly. Body text everywhere stays plain and legible.

![[gui-font-specimens.png]]

## Font roles

| Role | Typical Roblox faces | Style recipe | Seen in |
|---|---|---|---|
| **Big numbers / money** | FredokaOne, LuckiestGuy, GothamBlack | white or green fill · UIStroke 2–3 px near-black · slight drop offset | 🔎 '$997,151,167/s' (Brainrot), '$89,121/s' (Steal An Egg), '$68,543B/S' (TFFA) |
| **Window titles** | LuckiestGuy, FredokaOne, Bangers | white fill · thick stroke · on coloured header bar | shop/index headers |
| **Rarity labels** | same display face | **UIGradient** per rarity; rainbow for Secret | 🔎 'SECRET', 'TREX EGG', 'CANDY' |
| **Competitive HUD** | GothamBlack / GothamBold (→ Montserrat), Oswald | no stroke, on translucent dark plate, tabular feel | [[RIVALS]] |
| **Horror** | SpecialElite, GrenzeGotisch, Creepster (titles only) | low saturation, grain, small sizes | 🔎 Forsaken logo, survival timers |
| **Body / settings** | SourceSans, Builder Sans, Nunito | regular weight, no stroke, high contrast | descriptions, settings |

> [!note] Roblox font facts
> - `Enum.Font.Gotham*` renders with **Montserrat** glyphs on current Roblox (a licensing swap) — pick by weight (Medium/Bold/Black) and preview in Studio.
> - Use **`TextLabel.FontFace = Font.new(...)`** to select weights (e.g. `Font.fromEnum(Enum.Font.FredokaOne)` or `Font.new("rbxasset://fonts/families/GothamSSm.json", Enum.FontWeight.Black)`).
> - Roblox's own UI face is **Builder Sans** (`rbxasset://fonts/families/BuilderSans.json`) — great for body text.

## The rarity type system

![[gui-rarity-ladder.png]]

## Number formatting

![[gui-number-format.png]]

## Instructions

1. **Two families max**: one display face (FredokaOne *or* LuckiestGuy) + one body face (Builder Sans / SourceSans / Nunito).
2. **Outline every display string** with `UIStroke` (Thickness 2–3, Color #0D1017, LineJoinMode Round) — this is what makes text readable over any 3D background.
3. **Gradient only for meaning** (rarity, premium, events). Green = money, gold = premium currency, red = danger.
4. **Minimum sizes on phone**: body ≥ 14 pt, numbers ≥ 18 pt, titles ≥ 28 pt at 844×390 reference.
5. **Use `TextScaled` only inside size-constrained boxes** + `UITextSizeConstraint` (MaxTextSize) so desktop text doesn't balloon.
6. **Abbreviate big numbers** to 3 significant digits + suffix; full value in tooltips.
7. **Uppercase for buttons and titles**, sentence case for descriptions.

Reference sheet: [[Roblox Fonts Cheat Sheet]] · Related: [[GUI & Menus]] · [[HUD Design]]
