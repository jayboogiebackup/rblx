---
tags: [playbook, gameplay, luau]
---

# 🛠️ Playbook — Throw Arc & Power Meter

> [!summary] Goal
> The [[Throw Food For Animals]] verb: hold to charge a 0–20 meter, see the arc and landing ring, release to throw; the server decides distance from your Throw Power stat and spawns the reward in the zone where it lands.

![[hud-throw-food-for-animals.jpg]]
![[anno-tffa-arc.jpg]]

## Step 1 — Meter (client)

Ping-pong a value 0 → 20 → 0 while the button is held; release locks it.

```lua
-- StarterPlayerScripts/ThrowInput.client.lua (excerpt)
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")

local METER_MAX = 20
local CYCLE_SECONDS = 1.2 -- one sweep 0 → 20

local charging, startedAt = false, 0

local function meterValue(): number
	local t = (os.clock() - startedAt) / CYCLE_SECONDS
	local phase = t % 2 -- 0..2
	local p = phase <= 1 and phase or 2 - phase -- ping-pong 0..1..0
	return p * METER_MAX
end

local function begin() charging, startedAt = true, os.clock() end
local function release()
	if not charging then return end
	charging = false
	game.ReplicatedStorage.Remotes.Throw:FireServer(meterValue())
end

UserInputService.InputBegan:Connect(function(input, processed)
	if processed then return end
	if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
		begin()
	end
end)
UserInputService.InputEnded:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
		release()
	end
end)

RunService.RenderStepped:Connect(function()
	if charging then
		-- update the HUD needle: Needle.Position = UDim2.fromScale(meterValue() / METER_MAX, 0.5)
		-- update the arc preview with the predicted velocity (Step 2)
	end
end)
```

## Step 2 — Arc preview + landing ring (client)

Sample the projectile path `p(t) = origin + v·t + ½·g·t²` and raycast between samples to find the landing point.

```lua
local function sampleArc(origin: Vector3, velocity: Vector3, params: RaycastParams)
	local g = Vector3.new(0, -workspace.Gravity, 0)
	local points, prev = { origin }, origin
	local dt = 0.05
	for i = 1, 200 do -- up to 10 s of flight
		local t = i * dt
		local p = origin + velocity * t + 0.5 * g * t * t
		local hit = workspace:Raycast(prev, p - prev, params)
		if hit then
			table.insert(points, hit.Position)
			return points, hit.Position
		end
		table.insert(points, p)
		prev = p
	end
	return points, nil
end
```

Render: a pool of ~40 small Neon spheres (yellow `#FFD23F`, CanCollide/CanQuery/CanTouch off) placed on every 5th point, or Beams between Attachments; a flat cylinder ring at the landing point. Colour the arc by the zone it lands in to tease rarity.

## Step 3 — Velocity from stat (server decides)

```lua
-- ServerScriptService/Systems/Throwing.server.lua (excerpt)
local BASE_SPEED, SPEED_PER_POWER, ANGLE = 40, 0.08, math.rad(35)
local COOLDOWN = 0.8
local lastThrow = {}

game.ReplicatedStorage.Remotes.Throw.OnServerEvent:Connect(function(player, meter)
	if typeof(meter) ~= "number" or meter ~= meter then return end -- reject NaN/garbage
	meter = math.clamp(meter, 0, 20)
	local now = os.clock()
	if lastThrow[player] and now - lastThrow[player] < COOLDOWN then return end
	lastThrow[player] = now

	local root = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
	if not root then return end
	local power = player:GetAttribute("ThrowPower") or 0
	local speed = (BASE_SPEED + power * SPEED_PER_POWER) * (meter / 20)
	local flat = (root.CFrame.LookVector * Vector3.new(1, 0, 1)).Unit
	local dir = (CFrame.lookAt(Vector3.zero, flat) * CFrame.Angles(ANGLE, 0, 0)).LookVector
	local velocity = dir * speed

	-- same math as the client → landing point → zone → animal roll by food tier
	local landing = predictLanding(root.Position + Vector3.new(0, 2, 0), velocity) -- your sampleArc wrapper
	local zone = zoneAt(landing) -- e.g. by distance bands from the throw line
	spawnFoodAndAnimal(player, landing, zone, player:GetAttribute("EquippedFood"))
end)
```

> [!warning] Never trust the client's position or power
> The client sends **only the meter value**. Distance comes from the server's stat; landing is recomputed server-side.

## Step 4 — Training (pull-ups)

- A pull-up bar `ProximityPrompt` (hold) → play a rep animation → server adds XP (`x2 Training Power` pass doubles it, ✅ R$ 149 in TFFA) → level up adds Throw Power (📰 +5 per level).
- Each rep: "+XP" popup, bar fill, level-up burst. See [[Playbook - Juice & Animation Recipes]].

## Step 5 — Zones by distance

- Lay zones as **bands** along the throw lane; store `MinDistance` attributes on zone parts.
- Show the next zone's requirement in the top banner ("next: ✨ CELESTIAL at 2,000 power").
- Each zone has its own animal table; **food tier** filters which rarities can appear.
