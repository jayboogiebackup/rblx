---
tags: [playbook, hud, ui, luau]
---

# 🛠️ Playbook — Build a Mobile-First HUD

> [!summary] Goal
> Build an Archetype-A simulator HUD (currency + rate + stat, left menu grid, top timers, bottom hotbar/meter, toasts) that looks right on a phone and scales cleanly to desktop and console. Reference: [[HUD Design]] · [[hud-steal-an-egg.jpg]]

![[gui-mobile-safe-zones.png]]

## Step 1 — Set up the ScreenGui

In **StarterGui**, create `HUD` (ScreenGui):

| Property | Value | Why |
|---|---|---|
| `ResetOnSpawn` | `false` | HUD survives respawns (no flicker, no lost state). |
| `IgnoreGuiInset` | `false` | Keeps you below the Roblox top bar. |
| `ScreenInsets` | `CoreUISafeInsets` | Avoids notches **and** Roblox core UI. |
| `ZIndexBehavior` | `Sibling` | Predictable layering. |

Add a `UIScale` child (driven by the script in Step 3).

## Step 2 — Build the hierarchy

```text
HUD (ScreenGui)
├─ UIScale
├─ TopLeft      Frame  AnchorPoint(0,0)   Position {0,12},{0,12}    UIListLayout (vertical, 6 px)
│  ├─ CashPill      ImageLabel/Frame + UICorner(1,0) + UIStroke + TextLabel "$1.42M"
│  ├─ RateLabel     TextLabel "+$12,480/s"  (green, UIStroke)
│  └─ StatPill      "Speed 2,450"
├─ LeftMenu     Frame  AnchorPoint(0,0.5) Position {0,12},{0.5,0}   UIGridLayout CellSize {0,96},{0,84} CellPadding {0,12},{0,16}
│  ├─ ShopButton  (green)   ├─ IndexButton (blue)
│  ├─ PassButton  (purple)  └─ FreeButton  (gold, badge)
├─ TopCenter    Frame  AnchorPoint(0.5,0) Position {0.5,0},{0,8}    timers / event banner
├─ BottomCenter Frame  AnchorPoint(0.5,1) Position {0.5,0},{1,-12}  hotbar / meter / state banner
└─ Toasts       Frame  AnchorPoint(1,0)   Position {1,-12},{0,90}   UIListLayout (vertical, newest on top)
```

> [!tip] Use **Scale** for positions (anchored to screen edges) and **Offset** for sizes — then let `UIScale` handle device size. Add a `UIAspectRatioConstraint` to every square button.

## Step 3 — Scale for every screen

```lua
-- StarterPlayer/StarterPlayerScripts/HUDScale.client.lua
local Players = game:GetService("Players")

local hud = Players.LocalPlayer:WaitForChild("PlayerGui"):WaitForChild("HUD")
local uiScale = hud:WaitForChild("UIScale")

local REFERENCE = Vector2.new(844, 390) -- design canvas: phone in landscape
local MIN_SCALE, MAX_SCALE = 0.75, 1.5

local function update()
	local viewport = workspace.CurrentCamera.ViewportSize
	local s = math.min(viewport.X / REFERENCE.X, viewport.Y / REFERENCE.Y)
	uiScale.Scale = math.clamp(s, MIN_SCALE, MAX_SCALE)
end

workspace.CurrentCamera:GetPropertyChangedSignal("ViewportSize"):Connect(update)
update()
```

## Step 4 — The 'juicy' button component

![[gui-button-anatomy.png]]

Build one button in Studio, then reuse it:

1. `TextButton` (or `ImageButton`), `AnchorPoint = (0.5, 0.5)` so it scales around its center. Inside a layout, wrap it in a holder `Frame`.
2. `UICorner` CornerRadius `0.18` (scale).
3. `UIGradient` Rotation `90`, Color `#7DFF5C → #25B52A` (green example).
4. `UIStroke` Thickness `3`, Color `#0D1017`, `ApplyStrokeMode = Border`.
5. A darker `Frame` behind it offset `+5 px` Y = the 3D edge.
6. Icon `ImageLabel` + `TextLabel` (FredokaOne, white, its own `UIStroke` 2.5).

```lua
-- ReplicatedStorage/UI/JuicyButton.lua
local TweenService = game:GetService("TweenService")

local HOVER = TweenInfo.new(0.12, Enum.EasingStyle.Quad, Enum.EasingDirection.Out)
local PRESS = TweenInfo.new(0.06, Enum.EasingStyle.Quad, Enum.EasingDirection.Out)
local RELEASE = TweenInfo.new(0.18, Enum.EasingStyle.Back, Enum.EasingDirection.Out)

local JuicyButton = {}

function JuicyButton.attach(button: GuiButton, onClick: () -> ())
	local scale = button:FindFirstChildOfClass("UIScale") or Instance.new("UIScale")
	scale.Parent = button

	local function tweenTo(info: TweenInfo, value: number)
		TweenService:Create(scale, info, { Scale = value }):Play()
	end

	button.MouseEnter:Connect(function() tweenTo(HOVER, 1.06) end)
	button.MouseLeave:Connect(function() tweenTo(HOVER, 1) end)
	button.MouseButton1Down:Connect(function() tweenTo(PRESS, 0.92) end)
	button.MouseButton1Up:Connect(function() tweenTo(RELEASE, 1) end)
	button.Activated:Connect(onClick) -- fires for mouse, touch and gamepad
end

return JuicyButton
```

## Step 5 — Currency + rate display

```lua
-- ReplicatedStorage/Util/NumberFormat.lua
local SUFFIXES = { "", "K", "M", "B", "T", "Qa", "Qi", "Sx", "Sp", "Oc", "No", "Dc" }

local NumberFormat = {}

function NumberFormat.abbreviate(n: number): string
	local negative = n < 0
	n = math.abs(n)
	local i = 1
	while n >= 1000 and i < #SUFFIXES do
		n /= 1000
		i += 1
	end
	local text
	if i == 1 then
		text = tostring(math.floor(n))
	elseif n >= 100 then
		text = string.format("%d", math.floor(n))
	elseif n >= 10 then
		text = string.format("%.1f", math.floor(n * 10) / 10)
	else
		text = string.format("%.2f", math.floor(n * 100) / 100)
	end
	if text:find("%.") then -- trim trailing zeros: 1.20 → 1.2, 3.00 → 3
		text = text:gsub("0+$", ""):gsub("%.$", "")
	end
	return (negative and "-" or "") .. text .. SUFFIXES[i]
end

function NumberFormat.commas(n: number): string
	local s = tostring(math.floor(n))
	local formatted = s:reverse():gsub("(%d%d%d)", "%1,"):reverse()
	return (formatted:gsub("^,", ""))
end

return NumberFormat
```

Bind it to leaderstats/attributes on the client and **tween the number** (recipe in [[Playbook - Juice & Animation Recipes]]). Show **`+$X/s`** under the total — the rate is what keeps players playing.

## Step 6 — Timers from server time

Store end times on the server as attributes (e.g. `workspace:SetAttribute("EggRespawnAt", workspace:GetServerTimeNow() + 270)`) and render on the client:

```lua
local RunService = game:GetService("RunService")
local label = script.Parent -- TextLabel in TopCenter

RunService.Heartbeat:Connect(function()
	local endsAt = workspace:GetAttribute("EggRespawnAt")
	if not endsAt then return end
	local left = math.max(0, math.floor(endsAt - workspace:GetServerTimeNow()))
	label.Text = string.format("🥚 EGGS RESPAWN IN %d:%02d", left // 60, left % 60)
end)
```

## Step 7 — Toasts & alerts

- One `Toasts` list, newest first, max 3 visible, auto-dismiss after 3–4 s.
- Colour by type: green reward · red danger ("Someone is stealing…") · gold event · purple rare-pull announcement.
- Danger toasts also play a sound and can pulse the screen edge.

## Step 8 — Test matrix

- [ ] Studio **Device Emulator**: small phone, large phone, tablet, 1080p, 4K, console (10-foot).
- [ ] No button inside the thumbstick / jump / top-bar zones.
- [ ] Every button works with **touch, mouse and gamepad** (`Activated`, `GuiService.SelectedObject` for console).
- [ ] Text ≥ 14 pt at 844×390; numbers never overflow at 999.99Qa.
- [ ] HUD hides during cutscenes/reveals (`hud.Enabled = false`).

Spec it first: [[Template - HUD Spec]]
