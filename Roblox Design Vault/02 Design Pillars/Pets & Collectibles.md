---
tags: [pillar, pets, collection]
---

# 🐾 Pets & Collectibles

> [!summary]
> Six of the top 12 are built around collecting creatures (pets, animals, brainrots, fish). The winning formula: **a visible loot container → a dramatic reveal → a creature that *does something* (earns, follows, fights) → a reason to want the next tier.**

## How each game frames its collectible

| Game | Collectible | Comes from | Does what | Value multipliers |
|---|---|---|---|---|
| [[Steal An Egg]] | pets | eggs stolen from biome nests → hatch in pen | earns $/s | rarity × size × mutation (✅/📰) |
| [[Throw Food For Animals]] | animals | lured by thrown food | earns $/s in pen | food tier → rarity (📰) |
| [[Steal a Brainrot]] | brainrots | bought off a conveyor / stolen | earns $/s in base | rarity tiers up to Secret/OG (📰) |
| [[Pet Simulator 99]] | pets | eggs (multi-hatch) | breaks breakables | golden · rainbow · shiny · huge (✅) |
| [[Adopt Me]] | pets | eggs, events, trades | needs/aging, roleplay | age · neon · mega |
| [[Fish It]] | fish | cast & reel | sell, aquarium, log | rarity × mutation × weight (✅/📰) |

## The rarity ladder

![[gui-rarity-ladder.png]]

- Keep **the same colours everywhere**: billboards, egg tints, reveal rays, chat announcements, index frames.
- **Show odds** (🔎 TFFA thumbnails print '1 IN 999B'; 📰 Fish It guides list 1-in-millions odds). Odds *are* content; hiding them breeds confusion (📰 Steal An Egg guides disagree on mutation multipliers).

## The reveal

![[gui-hatch-sequence.jpg]]

## Design instructions

1. **Make the container collectible too** — eggs with patterns per biome (🔎 Steal An Egg), crates, mystery silhouettes.
2. **Give every collectible a job** (income, combat, follow). Pure-cosmetic pets retain worse in simulators.
3. **Stack 2–3 independent multipliers** (rarity × size × mutation) so duplicates are not duplicates.
4. **Use an Index** with silhouettes and completion rewards → [[GUI & Menus#Index / collection windows]].
5. **Announce rare pulls server-wide** (chat + banner) — social proof and FOMO.
6. **Plan duplicates**: combine (Adopt Me neon), sell, feed, or fuse.
7. **Seasonal variants** (Halloween, Candy) are the cheapest content drop you can make.
8. **Protect the economy**: if pets are tradable, never sell them directly for Robux at scale — sell *odds* and *time* (✅ PS99's passes are luck/automation, not pets).

Build steps: [[Playbook - Egg Hatch & Pet System]] · models: [[Playbook - Cube Pets & Variants]] · [[Playbook - Voxel Creatures]] · [[Playbook - Eggs & Loot Containers]]

Related: [[Models & Assets]] · [[Animation & Game Feel]] · [[Shops & Game Passes]]
