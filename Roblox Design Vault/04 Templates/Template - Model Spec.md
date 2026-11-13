---
tags: [template, models]
asset_class: "" # prop · container · building · common pet · hero pet · weapon · boss
style: "" # voxel · faceted low-poly · smooth stylised · cube-body · toy weapon · realism
status: "" # reference · blockout · model · texture · rig · in-game
---

# Model Spec — {{title}}

Reference: [[Model Budgets & Specs]] · [[Model Styles in Top Games]] · [[Playbook - Model Creation Pipeline]]

## Purpose
- What does it do in the game? (earns $/s, is stolen, is held, decorates…)
- Where is it seen most? (pen, first person, reveal screen, thumbnail)

## Targets

| Field | Target |
|---|---|
| Size (studs, W × H × L) | |
| Triangles | (see budget table) |
| Texture | palette · atlas · PBR ≤ 1024² |
| Bones | |
| Parts / meshes | |
| Pivot | feet · grip · base centre |
| Collision | Box · Hull · none |

## Silhouette
- [ ] Sketch / blockout attached
- [ ] Passes the 64 px black-shape test

## Variants
| Variant | Change (colour / material / texture / scale / mesh) |
|---|---|
| Base | |
| Golden | |
| Rainbow | |
| Event | |
| Huge | |

## Animations
| Clip | Length | Loop |
|---|---|---|
| Idle | | ✔ |
| | | |

## Done when
- [ ] In budget · imported at real scale · attributes set (`Rarity`, `Income`, `Variant`)
- [ ] Tested with 20+ copies on a phone
