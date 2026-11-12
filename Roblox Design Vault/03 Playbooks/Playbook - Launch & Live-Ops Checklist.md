---
tags: [playbook, live-ops, launch]
---

# 🛠️ Playbook — Launch & Live-Ops Checklist

> [!summary]
> The top games are run like live services: launch fast, patch daily in week one, ship weekly, run appointment events, and keep the store page in sync. Evidence: ✅ every top-12 game was updated within ~a week of the snapshot; ✅ most carry an emoji/update tag in the title ([[Live Chart Snapshot 2026-11-12]]).

## Pre-launch

- [ ] Core loop playable in **10 s**; first reward in **30 s** ([[Intuitiveness & Onboarding]]).
- [ ] HUD tested on phone / tablet / desktop / console ([[Playbook - Build a Mobile-First HUD]]).
- [ ] **2 passes + 3–6 products** live and tested in a private server ([[Playbook - Shop & Game Pass System]]).
- [ ] Store page: icon, **6 thumbnails in one template**, verb-first title, emoji how-to description ([[Playbook - Thumbnails & Store Page]]).
- [ ] **Group** created; in-game reward for like + favorite + join (📰 Steal An Egg: 10,000 Speed).
- [ ] Analytics: custom events for the onboarding funnel (spawn → first verb → first reward → first upgrade → first purchase prompt) via `AnalyticsService`.
- [ ] Data saving with retries + session locking; test rejoin, server shutdown, purchase during shutdown.
- [ ] Anti-exploit basics: server-authoritative economy, remote rate limits, sanity checks.

## Launch week

- [ ] Hotfix daily; post patch notes in the group.
- [ ] Add a title tag for the first update (`[UPD 1]`).
- [ ] Watch: **D1 retention, average session length, % reaching the first upgrade, purchase conversion**.
- [ ] Respond to the first guide/video creators (they're your marketing).

## Weekly cadence (template)

| Day | Action |
|---|---|
| Mon–Wed | Build next content drop (zone / pets / weapon / event) |
| Thu | Private-server test, balance |
| Fri | New thumbnails for the drop; description + title tag |
| Sat | **Release + event** (📰 Steal An Egg's first Admin Abuse was a Saturday; 📰 guides observed back-to-back Sunday updates) |
| Sun | Monitor, hotfix, community highlights |

## Event playbook ("admin abuse" & seasonal)

1. **Announce the time in several regions** (📰 guides publish start times per region — do it yourself in-game and in the group).
2. **Server-wide modifiers**: x2 power/cash, rare spawns, raining eggs, admin-spawned bosses.
3. **Limited collectibles** that never return (✅ MM2 has 70 retired limited passes/items).
4. **Countdown in the HUD** during the week before.
5. **Clip-worthy moments** (giant spawns, chaos) — short-form video drives discovery.
6. Follow with a **retention hook** (new zone / pass / daily reward reset) so event players stay.

Plan each one with [[Template - Live Event Plan]].

## Signals to watch (Creator Hub analytics)

| Metric | Healthy direction | If bad, look at… |
|---|---|---|
| Play-through / click-through | ↑ | thumbnails, icon, title |
| D1 / D7 retention | ↑ | first 5 minutes, early goals, daily rewards |
| Session length | ↑ | appointment timers, playtime gifts |
| Conversion (payers / DAU) | ↑ | starter pack, contextual offers, pass value |
| Like ratio | ≥ 85% (all top-12 are 82.8–94.7%) | griefing, pay-to-win, bugs |
