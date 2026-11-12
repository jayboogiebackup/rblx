---
tags: [home, moc]
snapshot_date: 2026-11-12
---

# 🎮 Roblox Top Games — Design Vault

> [!abstract] What this is
> A design teardown of the games at the top of Roblox in **November 2026** — HUD, GUI, gameplay mechanics, intuitiveness, art style, maps, models, pets, animation, fonts, shops and game passes — with **real data** (Roblox API snapshot, 2026-11-12), **official store images**, **original annotated mockups**, and **step-by-step playbooks** with Luau code to build the same systems yourself.

![[gui-hud-archetypes.png]]

## 🧭 How to use this vault

1. **Start with [[Why Games Perform]]** — the six drivers shared by every top game.
2. **Pick the closest game** below and read its teardown (each follows the same 13 sections).
3. **Go deep on a pillar** (HUD, shop, art…) for cross-game rules and proven examples.
4. **Build it** with the playbooks; plan with the templates (set *Settings → Templates → folder* to `04 Templates` — already configured).
5. Open **[[Design Map.canvas|the canvas]]** for a visual map of how everything connects.

> [!note] Confidence legend (used on every claim)
> ✅ **official Roblox data** (API, store description, pass text) · 📰 **third-party guides** (may be outdated/conflicting) · 🔎 **observed in official store images** · 🧠 **design analysis / genre convention** — verify in-game.
> HUD 'layout studies' are **reconstructed mockups**, clearly labelled on each image, not in-game screenshots.

## 🏆 The top-12 teardowns

| | Game | Top Playing rank | Players (snapshot) | Like % | Genre | Why it's up there (one line) |
|:--:|---|:--:|--:|--:|---|---|
| ![[steal-an-egg_icon.png\|48]] | [[Steal An Egg]] | #1 | 628,983 | 91.4% | Steal-tycoon + pets | Fuses steal-tycoon, egg hatching and speed training; 7-player rivalry |
| ![[brookhaven_icon.png\|48]] | [[Brookhaven RP]] | #2 | 374,701 | 85.9% | Roleplay | The world is the game; sells toys and spaces |
| ![[blox-fruits_icon.png\|48]] | [[Blox Fruits]] | #3 | 335,144 | 92.3% | Anime RPG | Level 3000 power fantasy + hourly fruit spawns |
| ![[throw-food-for-animals_icon.png\|48]] | [[Throw Food For Animals]] | #4 | 233,220 | 94.4% | Distance sim + pets | One verb (throw) + the clearest progress bar (distance) |
| ![[murder-mystery-2_icon.png\|48]] | [[Murder Mystery 2]] | #5 | 201,273 | 90.8% | Social deduction | Random roles + limited knives + trading, since 2014 |
| ![[adopt-me_icon.png\|48]] | [[Adopt Me]] | #6 | 159,514 | 86.4% | Pet care | Nurturing + trading + weekly events |
| ![[rivals_icon.png\|48]] | [[RIVALS]] | #7 | 120,246 | 93.6% | Duel FPS | Duel pads, first-to-5, fair cosmetics, consoles |
| ![[99-nights_icon.png\|48]] | [[99 Nights in the Forest]] | #8 | 115,838 | 90.5% | Co-op survival horror | A goal in the title + a campfire to protect |
| ![[steal-a-brainrot_icon.png\|48]] | [[Steal a Brainrot]] | #9 | 90,421 | 85.1% | Steal-tycoon | The template behind the 'Steal a ___' wave |
| ![[fish-it_icon.png\|48]] | [[Fish It]] | #14 | 65,483 | 82.8% | Fishing collectathon | Charge + reel skill check, luck ladder, 1M+ variants |
| ![[forsaken_icon.png\|48]] | [[Forsaken]] | #16 | 59,920 | 84.4% | Asymmetric horror | Roblox-folklore roster with kits |
| ![[pet-simulator-99_icon.png\|48]] | [[Pet Simulator 99]] | #20 | 51,864 | 94.7% | Pet collection | 3,000+ pets; sells luck & automation |

➕ **What's rising:** [[Rising Games Nov 2026]] (Survive Your Ideas, Break and Steal an Egg, DONT SPLASH, Sweep The Moon, the ragdoll wave) · Full chart: [[Live Chart Snapshot 2026-11-12]]

## 🧱 Design pillars (cross-game rules + proven examples)

| Pillar | You'll learn |
|---|---|
| [[HUD Design]] | 4 HUD archetypes, 10 rules, 12 per-game layout studies |
| [[GUI & Menus]] | Shop, index, reveal, rebirth, daily rewards, world-space UI, button anatomy |
| [[Core Loops & Mechanics]] | Loop map of all 12, reusable loop modules, how to design yours |
| [[Intuitiveness & Onboarding]] | 5-point rubric + scores, zero-text teaching, onboarding checklist |
| [[Art Style]] | The five styles at the top, palettes, lighting/material recipes |
| [[Maps & World Building]] | Map shapes, server size as design, building rules |
| [[Models & Assets]] | Asset multiplication patterns, detail budgets |
| [[Pets & Collectibles]] | Collectible framing, rarity ladder, reveal, duplicates |
| [[Animation & Game Feel]] | Where juice goes, timing cheat-sheet |
| [[Fonts & Typography]] | Font roles, outline & gradient recipes, number formatting |
| [[Shops & Game Passes]] | What 117 real passes say, 11 pass archetypes, pricing rules |
| [[Thumbnails & Icons]] | Annotated store art, series templates, title tags |
| [[Why Games Perform]] | Scoreboard + the six performance drivers |

## 🛠️ Playbooks (step-by-step, with Luau)

- [[Playbook - Build a Mobile-First HUD]]
- [[Playbook - Shop & Game Pass System]]
- [[Playbook - Egg Hatch & Pet System]]
- [[Playbook - Steal-a-X Base Loop]]
- [[Playbook - Throw Arc & Power Meter]]
- [[Playbook - Build a Map That Performs]]
- [[Playbook - Juice & Animation Recipes]]
- [[Playbook - Thumbnails & Store Page]]
- [[Playbook - Launch & Live-Ops Checklist]]

## 📚 Reference & data

- [[Live Chart Snapshot 2026-11-12]] — top 30 playing / trending / up-and-coming
- [[Game Pass Database]] — every pass with icon, price, description
- [[Color Palettes]] — measured hex palettes
- [[Roblox Fonts Cheat Sheet]] · [[Glossary]] · [[Sources]]
- [[Visual Index]] — every image in one place

## 🧩 Templates

[[Template - Game Teardown]] · [[Template - HUD Spec]] · [[Template - Game Pass Spec]] · [[Template - Live Event Plan]]

## 🔑 Ten key findings

1. **The #1 game is a fusion**: [[Steal An Egg]] = steal-tycoon + egg hatching + stat training. Fork proven loops, change one verb.
2. **The best-liked top-10 game has one verb**: [[Throw Food For Animals]] (94.4%) — throw.
3. **Theft games run tiny servers** (✅ 5–8 players); social games run 30–40.
4. **Always show the rate** ("+$12.4K/s") — the number every simulator thumbnail sells.
5. **Persistent HUD ≤ ~6 elements**; state gets temporary loud UI; money info lives in world-space billboards.
6. **New hits launch with just 2 passes** (x2 on each core clock); mature games run ladders and limited-time items.
7. **Median game pass: R$ 349; 32% of prices end in 99** ([[Game Pass Database]]).
8. **Rarity is a colour language** — grey → green → blue → purple → gold → red → rainbow — used everywhere.
9. **Store art = one verb + a prize + a threat + a 'YOU!' marker**, shipped as a series template for A/B tests.
10. **Live-ops cadence wins**: weekly drops, admin-abuse events, emoji update tags in titles ✅.
