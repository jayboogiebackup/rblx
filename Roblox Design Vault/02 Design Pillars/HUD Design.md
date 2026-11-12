---
tags: [pillar, hud, ui]
---

# 🧭 HUD Design

> [!summary] The rule the top 12 all follow
> **Persistent HUD = only what changes your next decision.** Everything else is either *world-space* (above objects), *temporary* (state banners, toasts) or *one tap away* (menus). Top simulators show ~5–8 persistent elements; competitive and horror games show fewer; roleplay games show almost none.

![[gui-hud-archetypes.png]]

## The four archetypes

### Archetype A — steal / tycoon simulator
*[[Steal An Egg]] · [[Steal a Brainrot]] · [[Throw Food For Animals]] · [[Pet Simulator 99]] · [[Fish It]]*

| Zone | What lives there | Example |
|---|---|---|
| Top-left (under the Roblox top bar) | Currency + **rate (/s)** + the one progression stat | $1.42M · +$12,480/s · Speed 2,450 |
| Left edge | 2×2 or 2×3 **menu grid**: Shop (green, first), Index, Passes/Rewards, Teleport | SHOP · INDEX · TRAILS · FREE |
| Top-center | **Timers**: respawn, event, next zone | "Eggs respawn in 4:21" |
| Center | **Clear** — gameplay | — |
| Bottom-center | Hotbar / meter / state banner | throw meter, "CARRYING…" |
| Right edge | Alerts, boosts, quests | "Someone is stealing your…" |
| World-space | Billboards: name / rarity / $ per second; lock timers; prompts | see [[gui-world-space-kit.png]] |

![[hud-steal-an-egg.jpg]]

### Archetype B — competitive FPS
*[[RIVALS]]* — score/round/timer top-center, kill feed top-right, crosshair center, health + loadout bottom-center, ammo bottom-right. **No currency, no menus mid-round.**

![[hud-rivals.jpg]]

### Archetype C — social / roleplay
*[[Brookhaven RP]] · [[Adopt Me]]* — an icon rail on one side, contextual panels, needs/tasks on the other side, and an **empty center** — the world is the content.

![[hud-brookhaven.jpg]]

### Archetype D — survival / horror / asymmetric
*[[99 Nights in the Forest]] · [[Forsaken]] · [[Murder Mystery 2]]* — big timer/day counter top-center, team status top-left, health/stamina/hunger bottom, abilities bottom-right, and **darkness, vignette and audio as HUD**.

![[hud-forsaken.jpg]]

## 10 HUD rules distilled from the top 12

1. **Design for a phone in landscape first** (844×390 pt). Desktop is the scale-up. ![[gui-mobile-safe-zones.png]]
2. **Never place buttons in Roblox's zones**: top bar (top-left), thumbstick (bottom-left), jump (bottom-right).
3. **Always show the rate, not just the total** ("+$12.4K/s"). Growth you can feel is the retention engine of every simulator.
4. **Menus dock to one edge** (usually left) in a 2-column grid; the first and greenest button is the Shop.
5. **State gets temporary, loud UI** (carrying, being robbed, role reveal) — not permanent widgets.
6. **Put money info in the world**, not the HUD: billboards over units with name / rarity / $ per second.
7. **Use notification badges** (red dot + count) to pull players into Rewards, Index and Rebirth.
8. **One meter per verb** (throw meter, cast charge, reel bar) at bottom-center, thumb-reachable.
9. **Big numbers need formatting**: 3 significant digits + suffix (K, M, B, T, Qa…). ![[gui-number-format.png]]
10. **Competitive = minimal; casual = juicy.** Match density to the genre (see archetypes).

## Per-game HUD studies

| Game | Archetype | Study |
|---|---|---|
| [[Steal An Egg]] | A | [[hud-steal-an-egg.jpg]] |
| [[Throw Food For Animals]] | A | [[hud-throw-food-for-animals.jpg]] |
| [[RIVALS]] | B | [[hud-rivals.jpg]] |
| [[Steal a Brainrot]] | A | [[hud-steal-a-brainrot.jpg]] |
| [[Brookhaven RP]] | C | [[hud-brookhaven.jpg]] |
| [[Blox Fruits]] | A/RPG hybrid | [[hud-blox-fruits.jpg]] |
| [[Murder Mystery 2]] | D | [[hud-murder-mystery-2.jpg]] |
| [[Adopt Me]] | C | [[hud-adopt-me.jpg]] |
| [[99 Nights in the Forest]] | D | [[hud-99-nights.jpg]] |
| [[Fish It]] | A | [[hud-fish-it.jpg]] |
| [[Pet Simulator 99]] | A | [[hud-pet-simulator-99.jpg]] |
| [[Forsaken]] | D | [[hud-forsaken.jpg]] |

> [!warning] About these images
> The HUD studies are **reconstructed layout mockups** (labelled on every image), built from official descriptions, pass text, guides and genre conventions — not in-game screenshots. Verify exact positions in the live game before cloning a layout pixel-for-pixel.

## Build it

→ [[Playbook - Build a Mobile-First HUD]] · [[Template - HUD Spec]] · [[GUI & Menus]] · [[Fonts & Typography]]
