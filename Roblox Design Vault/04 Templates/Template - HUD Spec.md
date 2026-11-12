---
tags: [template, hud]
game: ""
archetype: "" # A simulator · B FPS · C social · D survival
reference_resolution: "844x390 (phone landscape)"
---

# HUD Spec — {{title}}

Reference: [[HUD Design]] · [[gui-mobile-safe-zones.png]] · [[Playbook - Build a Mobile-First HUD]]

## Persistent elements (max ~6)

| # | Element | Zone | Data source | Update rate | Phone size | Notes |
|--:|---|---|---|---|---|---|
| 1 | Currency + rate | Top-left | `leaderstats.Cash`, attr `Rate` | 1 s tween | 42 px pill | |
| 2 | Primary stat | Top-left | attr | on change | | |
| 3 | Menu grid | Left | — | — | 96×84 cells | Shop first, green |
| 4 | Timers | Top-center | server attrs | Heartbeat | | |
| 5 | Hotbar / meter | Bottom-center | — | — | 62 px slots | |
| 6 | Toasts | Right | remote | event | | max 3 |

## Temporary / state UI

| State | Trigger | UI | Exit |
|---|---|---|---|
| Carrying | server attr `Carrying` | red banner + distance | deposit / drop |
| Rare pull | hatch result ≥ Legendary | reveal + server banner | tap / 2.5 s |

## World-space UI

| Object | Billboard content | Max distance | Notes |
|---|---|---|---|
| Pet/unit | name · rarity gradient · $/s | 60 studs | |
| Base door | lock countdown | 120 studs | |

## Checks
- [ ] Nothing in thumbstick / jump / top-bar zones
- [ ] Works with touch, mouse, gamepad
- [ ] Text ≥ 14 pt at reference resolution
- [ ] Numbers formatted (3 sig. digits + suffix)
- [ ] Colour = function (green buy · red close/danger · gold premium · blue info · purple rare)
