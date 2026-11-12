---
tags: [pillar, art, assets]
---

# 🧱 Models & Assets

> [!summary]
> The top games ship **lots of content fast** by building **systems that multiply a few assets**: one body template × colours × accessories × effects. Detail goes into *hero* assets (the rare pet, the legendary egg, the weapon in first person); filler stays simple.

## Asset multiplication patterns

| Pattern | Example | Multiplier |
|---|---|---|
| **Body template + variations** | [[Pet Simulator 99]] cube pets (✅ 3,000+ pets) | colour × ears × accessories × effects |
| **Rarity / mutation recolours** | [[Steal An Egg]] mutations, [[Fish It]] mutations, [[Steal a Brainrot]] Candy/Halloween variants | 1 mesh → 5–10 variants |
| **Size as a stat** | Steal An Egg egg sizes (✅), Fish It weights | 1 mesh → continuous range |
| **Neon / mega combine** | [[Adopt Me]] | duplicates become upgrades |
| **Skins on a fixed weapon set** | [[RIVALS]] skins, wraps, charms | 1 weapon → dozens of cosmetics |
| **Character roster with kits** | [[Forsaken]] | each character = gameplay + cosmetics line |
| **Voxel kit** | [[Throw Food For Animals]], [[Steal a Brainrot]] | cubes → any animal/food in hours |

## Detail budget (🧠 guideline)

| Asset class | Where seen | Detail level |
|---|---|---|
| Hero collectible (legendary+) | Reveal screen, billboard, thumbnails | **High**: unique silhouette, glow/particles, idle animation |
| Common collectible | In pens, crowds | Medium: template + colour |
| Eggs / crates | Shop, world, reveal | **High** — the loot box you see before opening |
| Player tools (bat, rod, gun) | First/third person all session | High in first person, medium in third |
| Environment props | Background | Low; reuse; texture over geometry |
| Terrain | Everywhere | Simple materials, strong colour |

## Building instructions

1. **Design the template first** (pet body, egg, weapon base), get it approved in-game at phone scale, *then* make variants.
2. **Use `SurfaceAppearance` or colour-swappable textures** for recolour variants; keep mesh count low.
3. **Add a 'rarity shell'**: particles + Highlight/outline + light — reusable across any model to make it read Legendary/Secret.
4. **Name and tag assets by rarity in Studio** (Attributes: `Rarity`, `Income`, `Weight`) so systems read data, not names.
5. **Make every collectible animate**: idle bob, blink, happy jump on pickup — even voxel animals.
6. **Check triangle and texture budgets on a low-end phone** with 20+ units on screen (pens and swarms are the worst case).

Related: [[Pets & Collectibles]] · [[Art Style]] · [[Animation & Game Feel]]
