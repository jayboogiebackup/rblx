---
tags: [pillar, monetization, shop]
---

# 💎 Shops & Game Passes

> [!summary] What 117 real game passes say (✅ Roblox API, 2026-11-12)
> - **Median price R$ 349**; 58% of passes sit between R$ 100 and R$ 499.
> - **32% of prices end in 99**, another ~15% in 49.
> - The newest hits launch with **only 2 passes** ([[Steal An Egg]] 399/467, [[Throw Food For Animals]] 99/149) — permanent multipliers on the two core clocks.
> - Mature games run **ladders** (RIVALS R$ 59 → 1,425; PS99 175 → 3,250) and **limited-time** passes (MM2: 70 retired).
> Full data: [[Game Pass Database]].

![[chart-pass-price-bands.png]]
![[chart-pass-prices-by-game.png]]

## Pass archetypes (with real examples)

| Archetype | Real examples (price) | When to use |
|---|---|---|
| **Core multiplier (x2)** | Steal An Egg X2 MONEY! (399), X2 GROWTH SPEED! (467); TFFA x2 Cash (99), x2 Training Power (149); Brainrot 2x Money (299); Blox Fruits 2x Money (450) | Day one. One per core clock. |
| **Luck ladder** | Fish It Small Luck 50 → Extra Luck 245 → Advanced Luck 545; PS99 Lucky 275 → Ultra Lucky 800 | Collection games; same benefit, 3 wallets. |
| **Automation / convenience** | PS99 Auto Farm 175, Auto Tap 350; Fish It Sell Anywhere 315; Sweep The Moon Sell As You Sweep 249 | Remove friction you designed in on purpose. |
| **Capacity** | Adopt Me +1 Pet Pen Slot 295; PS99 +15 Pets 375, +15 Eggs 625; DONT SPLASH 4th/5th Tool Slot 99/149 | Players who are already invested. |
| **Information** | Blox Fruits Fruit Notifier 2,700 | When scarcity/timers exist. |
| **VIP bundle** | Brookhaven 749, Adopt Me 480, PS99 400, Fish It 445, Brainrot 375, Forsaken 599 | Status + small perks + chat tag. |
| **Toys / verbs** | Brookhaven Disaster Pass 375, On Demand Fire 40, Music Unlocked 199 | Sandbox/roleplay games. |
| **Content bundle** | RIVALS Starter 59 → Heavy Duty 1,425 (weapon + skin + charm) | Fair-play competitive games. |
| **Meta / rules** | Survive Your Ideas /admin 1,449, /god 499, /chaos 399 | Party games — sell *rule changes*. |
| **Whale anchor** | Steal a Brainrot Admin Commands **7,999** | Frames everything else as cheap. |
| **Limited-time** | MM2 "GODLY of the Month" (70 retired); Fish It ⏳ boats; DONT SPLASH Fall Pack "until November 14" | Scarcity + trading economies. |

## Pass walls (proven icon & naming examples)

![[wall-passes-simulators.png]]
![[wall-passes-social.png]]
![[wall-passes-combat.png]]

## Shop UI

![[gui-shop-window.png]]

## Pricing instructions

1. **Launch with 2–3 passes**: one x2 per core clock + (optional) VIP. Add more as systems appear.
2. **Price new/young-audience games low** (99–149) and established ones higher (299–499). Odd 'calculated' prices (467) are a valid test.
3. **Build a ladder** once you have 6+ items: entry < 100, core 199–499, premium 799–1,499, anchor 2,000+.
4. **Write descriptions like Sweep The Moon**: what changes, what doesn't, forever or not. ("Your back canister never fills… You still empty it at the intake to get paid.")
5. **Name with emoji + effect** (✅ PS99 "Ultra Lucky! 🍀✨", Fish It "Advanced Luck 🍀✨") and say **"(PERMANENT, STACKS)"** where true.
6. **Passes = permanent; developer products = consumables** (boosts, skips, currency packs, lucky blocks). Consumables scale with engagement.
7. **Never sell tradable collectibles directly** if you have a trading economy — sell odds and time.
8. **Show the value in play**: active boost chips on the HUD ("🍀 +150% Luck") remind buyers and advertise to everyone else.
9. **Starter pack with an anchor**: ✅ Adopt Me's retired "Only 99 R$! (items worth 560 R$)".

Implementation: [[Playbook - Shop & Game Pass System]] · Spec: [[Template - Game Pass Spec]]
