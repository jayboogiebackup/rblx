---
tags: [pillar, gui, ui]
---

# 🪟 GUI & Menus

> [!summary]
> Top-game menus share one visual grammar: **chunky rounded panels with a thick dark outline, a coloured header bar, a big red ✕, tabs as pill buttons, and cards with a big icon + one green price button.** It's not subtle and it's not meant to be — it reads on a 6-inch phone held by a 10-year-old.

## Shop windows

![[gui-shop-window.png]]

| # | Element | Rule |
|--:|---|---|
| 1 | **Header bar colour = button colour** | The green SHOP button opens a green-headed window → spatial memory. |
| 2 | **Tabs** (Passes · Cash · Boosts · Bundles) | Max 4–5; the active tab is gold. |
| 3 | **Ribbon** ("BEST VALUE", "POPULAR") | One per tab, tilted, red. |
| 4 | **Price button** — green, Robux glyph, outlined number | One action per card. |
| 5 | **Close ✕** — red, big, top-right | Never hide the exit (trust + store policy). |
| 6 | **Icon** — circular sunburst badge | See the pass icon formula below. |

**Pass icon formula** (✅ observed across 117 real passes — [[Game Pass Database]]): circular badge · radial sunburst in the category colour (gold = money, red = power, green = luck, purple = rare) · one bold central object · white "x2" with a black outline when it's a multiplier.

![[wall-passes-simulators.png]]

## Index / collection windows

![[gui-index-window.png]]

1. **Found / total counter** in the header ("8 / 12 found").
2. **Completion bar with a reward** ("+10% cash forever at 100%") — turns collecting into progression.
3. **Owned cards**: full colour, name, rarity label.
4. **Unfound cards**: black silhouette + "???" — curiosity gap; rarity frame still visible so you know what you're hunting.
5. **Secret tier**: rainbow frame even when unfound — the hype is the frame.

## Reveal & reward moments

![[gui-hatch-sequence.jpg]]

→ build steps in [[Playbook - Egg Hatch & Pet System]].

## Rebirth / prestige modals

![[gui-rebirth-modal.png]]

1. Title states the transition (**REBIRTH 4 → 5**).
2. **Lose** vs **Gain** side by side (red / green).
3. Gains are *permanent* and specific (×2.5 cash, +1 floor, exclusive pet, nameplate).
4. Requirements with ✔ / ✖ and a count.
5. Primary button disabled until requirements are met; secondary button is "NOT YET" — never shame the player.

## Daily rewards & playtime gifts

![[gui-daily-rewards.png]]

1. 7-day calendar with a **big day-7 reward** (exclusive pet) and a streak counter.
2. The claimable day glows; claimed days dim with ✔.
3. **Playtime gifts** at 5/10/15/25/40/60 minutes — session-length extenders.
4. Countdown on locked gifts so the next goal is always visible.

## World-space GUI (BillboardGui / SurfaceGui / ProximityPrompt)

![[gui-world-space-kit.png]]

## Button anatomy

![[gui-button-anatomy.png]]

## Rules

> [!tip] Copy these
> - **One component library**: button, panel, tab, card, toast. Same stroke, radius and shadow everywhere.
> - **Colour = function**: green = buy/confirm, red = close/danger, gold = premium/selected, blue = info/collection, purple = rare/rebirth.
> - **Every window opens with a pop** (scale 0.8 → 1.0, Back-Out, 0.18 s) and closes faster than it opens.
> - **Robux prices are always on a button**, never plain text.

Related: [[HUD Design]] · [[Fonts & Typography]] · [[Shops & Game Passes]] · [[Playbook - Build a Mobile-First HUD]]
