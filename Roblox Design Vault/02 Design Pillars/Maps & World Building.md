---
tags: [pillar, map, level-design]
---

# 🗺️ Maps & World Building

> [!summary]
> In top simulators **the map is the progress bar**: zones get harder and more colourful the farther you go, and you can *see* the next one before you can afford it. In social and competitive games the map is a **stage** (landmarks, lanes). Detail is spent where the camera looks; everything else is cheap.

## Map shapes used by the top 12

| Shape | Games | Diagram | Why |
|---|---|---|---|
| **Linear distance bands** | [[Throw Food For Animals]] | spawn ▶ zone 1 ▶ zone 2 ▶ … | Distance = progress; every boundary visible from the start. |
| **Hub + biome ring** | [[Steal An Egg]] | bases in the middle, biomes radiating out by difficulty | Risk grows with distance from home (the carry is the game). |
| **Ring of bases around a shop** | [[Steal a Brainrot]] | conveyor center, bases facing it | Everyone sees everyone's loot → envy → theft. |
| **Zone chain with purchasable gates** | [[Pet Simulator 99]] | zone ▶ gate ▶ zone | Currency sink + visible next goal. |
| **Archipelago / seas** | [[Blox Fruits]], [[Fish It]] | islands by level band, travel by boat | Travel time makes arrival feel earned; sells boats. |
| **Arena set** | [[RIVALS]], [[Murder Mystery 2]], [[Forsaken]] | many small maps, rotated per round | Variety per round; small = fast. |
| **Walkable town** | [[Brookhaven RP]], [[Adopt Me]] | landmarks + lots + roads | Landmarks are roleplay prompts. |
| **Procedural wilderness around a camp** | [[99 Nights in the Forest]] | campfire center, fog radius | Safety = light radius. |

![[throw-food-for-animals_thumb-1.jpg]]
*🔎 Throw Food For Animals literally draws its map as a progression strip: grass → meadow → desert → lava → void.*

## Server size is a map decision

✅ Max players at snapshot: Steal An Egg **7**, Throw Food For Animals **5**, Steal a Brainrot **8**, Pet Simulator 99 **10**, Blox Fruits **12**, MM2 **12**, Fish It **20**, 99 Nights **25**, Brookhaven **30**, Adopt Me **35**, RIVALS **40** (lobby).

🧠 Theft/rivalry games run **tiny servers** (5–8) so every rival is known and every base fits on screen; social games run **large servers** (30–40) so there's always an audience.

## Building instructions

1. **Draw the progression on paper first**: zones in order, the stat or price that gates each, and the *visual* change (colour, props, music) per zone.
2. **One dominant hue per zone** (desert yellow, ice white, lava red, void purple) — the player should know where they are from a single frame.
3. **Make gates visible**: walls, rings, glowing borders, signs with the requirement ("Need 2,000 Power").
4. **Keep the core lane clear**: no props where the verb happens (throw lane, carry path, duel sightlines).
5. **Detail density follows the camera**: hero props near spawn and goals; low-detail filler at the edges; skybox and fog to hide the end of the world.
6. **Landmarks every ~100 studs** in towns/hubs so players can give directions.
7. **Budget for phones** — enable `Workspace.StreamingEnabled`, reuse meshes (instances of one MeshPart share memory), prefer textures over geometry for small detail, avoid thousands of unanchored parts. Test on a low-end phone, not your PC.
8. **Ship new zones as updates** — a zone drop is the cheapest 'big update' (📰 TFFA shipped a new map ~7 weeks after launch).

Step-by-step: [[Playbook - Build a Map That Performs]]

Related: [[Art Style]] · [[Models & Assets]] · [[Core Loops & Mechanics]]
