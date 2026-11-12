---
tags: [playbook, monetization, luau]
---

# 🛠️ Playbook — Shop & Game Pass System

> [!summary] Goal
> A shop window like the top games' (tabs, cards, green Robux buttons), backed by a **server-authoritative** pass/product system that caches ownership, never trusts the client, and grants developer products exactly once. Strategy: [[Shops & Game Passes]] · Data: [[Game Pass Database]]

![[gui-shop-window.png]]

## Step 1 — Decide what's a pass vs a product

| Use a **Game Pass** (one-time, permanent) | Use a **Developer Product** (repeatable) |
|---|---|
| x2 Money, x2 Growth, Luck +%, VIP, Auto-farm, extra slots, cosmetics bundles | Time skips, boosts (15/30/60 min), currency packs, lucky blocks/eggs, revives |

Launch set used by the top new games: **2 passes** (one per core clock) + 3–6 products.

## Step 2 — Create items in the Creator Hub

1. Creator Hub → your experience → **Monetization → Passes / Developer Products**.
2. Upload a **512×512 icon** following the formula: circular badge, radial sunburst in the category colour, one bold object, white outlined "x2" (see [[wall-passes-simulators.png]]).
3. Name with effect + emoji ("x2 Cash 💰"), describe exactly what changes ("Double cash from every animal, forever!").
4. Copy each **ID** into a shared config module.

```lua
-- ReplicatedStorage/Config/Monetization.lua
return {
	Passes = {
		X2_MONEY = 0, -- replace with your pass IDs
		X2_GROWTH = 0,
	},
	Products = {
		SKIP_HATCH = 0,
		BOOST_LUCK_15M = 0,
		CASH_PACK_S = 0,
	},
}
```

## Step 3 — Server: ownership cache + attributes

```lua
-- ServerScriptService/Monetization/Passes.server.lua
local MarketplaceService = game:GetService("MarketplaceService")
local Players = game:GetService("Players")
local Config = require(game.ReplicatedStorage.Config.Monetization)

local function setOwned(player: Player, key: string, owned: boolean)
	player:SetAttribute("Pass_" .. key, owned) -- the client UI reads this
end

local function checkPasses(player: Player)
	for key, passId in Config.Passes do
		local ok, owns = pcall(MarketplaceService.UserOwnsGamePassAsync, MarketplaceService, player.UserId, passId)
		if ok then
			setOwned(player, key, owns)
		else
			warn("Pass check failed", key, owns)
		end
	end
end

Players.PlayerAdded:Connect(checkPasses)
for _, p in Players:GetPlayers() do task.spawn(checkPasses, p) end

-- Purchases made during the session
MarketplaceService.PromptGamePassPurchaseFinished:Connect(function(player, passId, purchased)
	if not purchased then return end
	for key, id in Config.Passes do
		if id == passId then setOwned(player, key, true) end
	end
end)
```

Use it in gameplay (server only):

```lua
local function cashMultiplier(player: Player): number
	return player:GetAttribute("Pass_X2_MONEY") and 2 or 1
end
```

## Step 4 — Server: developer products (grant exactly once)

```lua
-- ServerScriptService/Monetization/Products.server.lua
local MarketplaceService = game:GetService("MarketplaceService")
local DataStoreService = game:GetService("DataStoreService")
local Players = game:GetService("Players")
local Config = require(game.ReplicatedStorage.Config.Monetization)
local Hatchery = require(game.ServerScriptService.Systems.Hatchery) -- your own module

local purchaseHistory = DataStoreService:GetDataStore("PurchaseHistory")

-- Each handler returns true when the reward was granted.
local handlers = {
	[Config.Products.SKIP_HATCH] = function(player)
		return Hatchery.skipOne(player) -- must return true on success
	end,
	[Config.Products.BOOST_LUCK_15M] = function(player)
		local now = workspace:GetServerTimeNow()
		local current = math.max(player:GetAttribute("LuckBoostUntil") or 0, now)
		player:SetAttribute("LuckBoostUntil", current + 15 * 60)
		return true
	end,
}

MarketplaceService.ProcessReceipt = function(receipt)
	local key = receipt.PlayerId .. "_" .. receipt.PurchaseId
	local ok, recorded = pcall(function()
		return purchaseHistory:UpdateAsync(key, function(alreadyGranted)
			if alreadyGranted then
				return true -- granted before: keep the record, don't grant twice
			end
			local player = Players:GetPlayerByUserId(receipt.PlayerId)
			local handler = handlers[receipt.ProductId]
			if not player or not handler then
				return nil -- abort; Roblox will retry later
			end
			local granted, result = pcall(handler, player)
			if not granted or not result then
				return nil
			end
			return true
		end)
	end)
	if ok and recorded then
		return Enum.ProductPurchaseDecision.PurchaseGranted
	end
	return Enum.ProductPurchaseDecision.NotProcessedYet
end
```

> [!warning] Rules
> - **Only one script** may set `ProcessReceipt`.
> - Handlers run inside `UpdateAsync`'s callback, which **must not yield** — set attributes / in-memory data only, and let your normal save flow persist it.
> - **Never grant from the client**; the client only *prompts*.
> - Return `NotProcessedYet` on any failure — Roblox retries when the player rejoins.
> - Save the granted reward into the player's data in your normal save flow.

## Step 5 — Client: shop window

```lua
-- StarterPlayerScripts/Shop.client.lua (excerpt)
local MarketplaceService = game:GetService("MarketplaceService")
local Players = game:GetService("Players")
local Config = require(game.ReplicatedStorage.Config.Monetization)
local player = Players.LocalPlayer

local function fillPassCard(card: Frame, key: string)
	local passId = Config.Passes[key]
	local ok, info = pcall(MarketplaceService.GetProductInfo, MarketplaceService, passId, Enum.InfoType.GamePass)
	if ok then
		card.Title.Text = info.Name
		card.Price.Label.Text = tostring(info.PriceInRobux) -- always the live price
		card.Icon.Image = "rbxassetid://" .. info.IconImageAssetId
	end
	local function refresh()
		local owned = player:GetAttribute("Pass_" .. key)
		card.Price.Visible = not owned
		card.Owned.Visible = owned == true
	end
	player:GetAttributeChangedSignal("Pass_" .. key):Connect(refresh)
	refresh()
	card.Price.Activated:Connect(function()
		MarketplaceService:PromptGamePassPurchase(player, passId)
	end)
end
```

## Step 6 — Shop UX checklist

- [ ] Tabs: **Passes · Cash · Boosts · Bundles** (≤ 5).
- [ ] One **ribbon** per tab ("BEST VALUE").
- [ ] Owned passes show ✔ OWNED instead of a price.
- [ ] Active boosts appear as **HUD chips** with timers ("🍀 +150% Luck 14:22").
- [ ] Open the shop **contextually**: when a player can't afford something, offer the relevant pass/product once — never spam.
- [ ] Big red ✕; closes in 0.12 s.

Spec each item with [[Template - Game Pass Spec]].
