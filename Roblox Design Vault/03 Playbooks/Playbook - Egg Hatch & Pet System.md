---
tags: [playbook, pets, luau]
---

# 🛠️ Playbook — Egg Hatch & Pet System

> [!summary] Goal
> Eggs with weighted rarity tables, luck, size and mutation rolls (server), income per pet, and a 4-beat reveal (client). Pattern sources: [[Steal An Egg]] (rarity × size × mutation), [[Pet Simulator 99]] (luck passes, multi-hatch), [[Fish It]] (odds as content). Design: [[Pets & Collectibles]]

![[gui-hatch-sequence.jpg]]

## Step 1 — Data tables (ReplicatedStorage, read-only)

```lua
-- ReplicatedStorage/Data/Eggs.lua
return {
	ForestEgg = {
		price = 1_000,
		hatchSeconds = 60, -- grow timer in the pen (x2 Growth pass halves it)
		pets = {
			{ id = "Chicken", rarity = "Common",    weight = 60,   baseIncome = 5 },
			{ id = "Fox",     rarity = "Uncommon",  weight = 25,   baseIncome = 12 },
			{ id = "Panda",   rarity = "Rare",      weight = 10,   baseIncome = 30 },
			{ id = "Lion",    rarity = "Epic",      weight = 4,    baseIncome = 80 },
			{ id = "Dragon",  rarity = "Legendary", weight = 0.9,  baseIncome = 250 },
			{ id = "Hydra",   rarity = "Mythic",    weight = 0.1,  baseIncome = 1_200 },
		},
	},
}
```

```lua
-- ReplicatedStorage/Data/Rarity.lua
return {
	Order = { "Common", "Uncommon", "Rare", "Epic", "Legendary", "Mythic", "Secret" },
	Rank = { Common = 1, Uncommon = 2, Rare = 3, Epic = 4, Legendary = 5, Mythic = 6, Secret = 7 },
	Colors = { -- gradient top, bottom (see the rarity ladder)
		Common = { Color3.fromHex("eeeeee"), Color3.fromHex("9a9a9a") },
		Uncommon = { Color3.fromHex("a6ff7a"), Color3.fromHex("26b83a") },
		Rare = { Color3.fromHex("7fd8ff"), Color3.fromHex("246bff") },
		Epic = { Color3.fromHex("e19bff"), Color3.fromHex("8a2be2") },
		Legendary = { Color3.fromHex("ffe66b"), Color3.fromHex("ff8a1f") },
		Mythic = { Color3.fromHex("ff7aa8"), Color3.fromHex("e0123c") },
	},
}
```

![[gui-rarity-ladder.png]]

## Step 2 — Server roll: rarity × size × mutation

```lua
-- ServerScriptService/Systems/Hatchery.lua
local Eggs = require(game.ReplicatedStorage.Data.Eggs)
local Rarity = require(game.ReplicatedStorage.Data.Rarity)

local rng = Random.new()
local MUTATIONS = { -- chance, income multiplier
	{ name = "Rainbow", chance = 0.002, mult = 5 },
	{ name = "Golden",  chance = 0.02,  mult = 2 },
	{ name = "Silver",  chance = 0.08,  mult = 1.25 },
}

local Hatchery = {}

local function rollPet(egg, luck: number)
	local total, weights = 0, table.create(#egg.pets)
	for i, pet in egg.pets do
		local w = pet.weight
		if Rarity.Rank[pet.rarity] >= Rarity.Rank.Rare then
			w *= luck -- luck only boosts Rare and above
		end
		weights[i] = w
		total += w
	end
	local pick = rng:NextNumber(0, total)
	for i, w in weights do
		pick -= w
		if pick <= 0 then return egg.pets[i] end
	end
	return egg.pets[#egg.pets]
end

local function rollSize(): number
	-- most pets are normal size; big ones are rare (skewed curve)
	return 1 + 2 * rng:NextNumber() ^ 4 -- 1.0x … 3.0x
end

local function rollMutation(mutationBonus: number)
	for _, m in MUTATIONS do -- rarest first
		if rng:NextNumber() < m.chance * mutationBonus then
			return m
		end
	end
	return nil
end

function Hatchery.hatch(player: Player, eggId: string)
	local egg = assert(Eggs[eggId], "unknown egg")
	local luck = (player:GetAttribute("Pass_LUCKY") and 2 or 1)
		* ((player:GetAttribute("LuckBoostUntil") or 0) > workspace:GetServerTimeNow() and 1.5 or 1)
	local pet = rollPet(egg, luck)
	local size = rollSize()
	local mutation = rollMutation(1)
	local income = pet.baseIncome * size * (mutation and mutation.mult or 1)
	return {
		id = pet.id,
		rarity = pet.rarity,
		size = math.floor(size * 100) / 100,
		mutation = mutation and mutation.name or nil,
		income = math.floor(income),
	}
end

return Hatchery
```

> [!tip] Publish the odds
> Show each egg's table (and current luck) in the egg's BillboardGui or a tooltip. Players and guide-writers will compute it anyway — 📰 Steal An Egg guides disagree on mutation numbers because they're hidden.

## Step 3 — Client reveal (4 beats)

```lua
-- StarterPlayerScripts/HatchReveal.client.lua (excerpt)
local TweenService = game:GetService("TweenService")
local Rarity = require(game.ReplicatedStorage.Data.Rarity)

local gui = script.Parent:WaitForChild("Reveal") -- ScreenGui with Egg (ImageLabel), Flash (Frame), Card (Frame)

local function reveal(result)
	local rank = Rarity.Rank[result.rarity]
	local anticipation = 0.6 + 0.1 * rank -- rarer = longer
	gui.Enabled = true

	-- 1. ANTICIPATION: wobble faster and faster
	local egg = gui.Egg
	local t0 = os.clock()
	while os.clock() - t0 < anticipation do
		local p = (os.clock() - t0) / anticipation
		egg.Rotation = math.sin(os.clock() * (10 + 30 * p)) * (8 + 10 * p)
		task.wait()
	end

	-- 2. CRACK: tint toward rarity colour
	TweenService:Create(egg, TweenInfo.new(0.3), { ImageColor3 = Rarity.Colors[result.rarity][1] }):Play()
	task.wait(0.3)

	-- 3. FLASH (hides the swap)
	gui.Flash.BackgroundTransparency = 0
	egg.Visible = false
	TweenService:Create(gui.Flash, TweenInfo.new(0.15), { BackgroundTransparency = 1 }):Play()

	-- 4. REVEAL: pop the card in with Back-Out
	local card = gui.Card
	card.PetName.Text = result.id
	card.RarityLabel.Text = string.upper(result.rarity)
	card.Income.Text = "$" .. result.income .. "/s"
	card.UIScale.Scale = 0.3
	card.Visible = true
	TweenService:Create(card.UIScale, TweenInfo.new(0.35, Enum.EasingStyle.Back, Enum.EasingDirection.Out), { Scale = 1 }):Play()
end
```

Add: spinning rays behind the card (rotate an ImageLabel forever), a rarity-specific sound, confetti `ParticleEmitter:Emit(40)` in a ViewportFrame or world, and a **server-wide announcement** for Legendary+ (chat + banner).

## Step 4 — Pets that earn

1. On hatch, store the pet in the player's data (`{id, rarity, size, mutation, income}`).
2. Place it in a pen slot (Model clone + `BillboardGui`: name / rarity gradient / `$X/s`).
3. Income tick on the server (see [[Playbook - Steal-a-X Base Loop#Step 4 — Income tick]]).

## Step 5 — Index & duplicates

- Index = set of `id..mutation` discovered; reward at completion % (see [[gui-index-window.png]]).
- Duplicates: sell, combine (3 → next tier), or feed for XP — never dead weight.
