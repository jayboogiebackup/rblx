---
tags: [pillar, animation, juice]
---

# ✨ Animation & Game Feel

> [!summary]
> 'Juice' is why a simple loop feels great. Top games animate **every number, every button and every reward**, and they save their biggest effects for the rarest moments. Players don't read your UI — they *feel* it.

## Where the top games spend animation

| Moment | Examples | Juice recipe |
|---|---|---|
| **Gaining money** | every simulator | floating "+$12,480" popups that rise & fade; counter tween; coin sound with pitch variance |
| **Rare reveal** | eggs, catches, units | anticipation wobble → flash → pop-in (Back-Out) → spinning rays → server announcement |
| **Core verb** | throw (TFFA), carry (Steal An Egg), cast/reel (Fish It), shoot (RIVALS) | wind-up, release, trail/arc, impact puff, camera nudge |
| **Getting hit / losing** | bat knock-back, MM2 death, Forsaken chase | ragdoll/knock-back, red flash, short slow-mo, sound sting |
| **Buttons** | all | hover grow, press squash, release bounce, click sound |
| **Windows** | shops, index, modals | scale 0.8 → 1 with Back-Out (≈0.18 s), close 0.12 s |
| **Idle** | pets, units, eggs | bob, blink, sway — nothing on screen should be fully still |

🔎 Store art shows the intended energy: egg lifted overhead, panic-running, crying when caught, straining on a fishing rod.

## Timing cheat-sheet (🧠 proven defaults)

| Effect | Duration | Easing |
|---|---|---|
| Button hover scale 1.0 → 1.06 | 0.10–0.12 s | Quad Out |
| Button press 1.0 → 0.92 | 0.06 s | Quad Out |
| Window open 0.8 → 1.0 | 0.18 s | Back Out |
| Window close 1.0 → 0.85 + fade | 0.12 s | Quad In |
| Number popup rise 40 px + fade | 0.6–0.8 s | Quad Out |
| Currency counter tween | 0.25 s | Quad Out |
| Reveal flash | 0.15 s | Linear |
| Rarity rays spin | loop 4–6 s/turn | Linear |
| Camera shake on impact | 0.15–0.3 s, amplitude 0.2–0.6 studs | decaying noise |

## Rules

1. **Rarer = longer & louder** — variable reward intensity is the dopamine curve.
2. **Always allow skipping** repeated animations after the first time in a session (multi-hatch, auto-open).
3. **Animate the cause and the effect**: the pull-up *and* the "+XP" *and* the level bar.
4. **Sound is half the juice** — distinct sounds per rarity; ascending pitch for streaks.
5. **Respect performance**: pool popups and particles; cap simultaneous effects on phones.
6. **Reduced-motion option** for screen shake and flashes (✅ Forsaken even warns about flashing lights in its description).

Recipes with code: [[Playbook - Juice & Animation Recipes]] · rigs & clips: [[Playbook - Rigging & Animating Models]]

Related: [[GUI & Menus]] · [[Pets & Collectibles]]
