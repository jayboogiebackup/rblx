---
tags: [playbook, animation, juice, luau]
---

# 🛠️ Playbook — Juice & Animation Recipes

> [!summary]
> Copy-paste recipes for the feedback every top game uses. Timings come from [[Animation & Game Feel#Timing cheat-sheet (🧠 proven defaults)]].

## 1. Counter that tweens instead of snapping

```lua
local TweenService = game:GetService("TweenService")
local NumberFormat = require(game.ReplicatedStorage.Util.NumberFormat)

local function tweenCounter(label: TextLabel, from: number, to: number)
	local value = Instance.new("NumberValue")
	value.Value = from
	value.Changed:Connect(function(v)
		label.Text = "$" .. NumberFormat.abbreviate(v)
	end)
	local tween = TweenService:Create(value, TweenInfo.new(0.25, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), { Value = to })
	tween.Completed:Once(function() value:Destroy() end)
	tween:Play()
end
```

## 2. Floating "+$" popup over a pet/pen (BillboardGui)

```lua
local function popup(adornee: BasePart, text: string, color: Color3)
	local gui = Instance.new("BillboardGui")
	gui.Size = UDim2.fromOffset(200, 50)
	gui.StudsOffset = Vector3.new(0, 3, 0)
	gui.AlwaysOnTop = true
	gui.Adornee = adornee
	local label = Instance.new("TextLabel")
	label.Size = UDim2.fromScale(1, 1)
	label.BackgroundTransparency = 1
	label.FontFace = Font.fromEnum(Enum.Font.FredokaOne)
	label.TextScaled = true
	label.TextColor3 = color
	label.Text = text
	local stroke = Instance.new("UIStroke")
	stroke.Thickness = 2
	stroke.Color = Color3.fromHex("0d1017")
	stroke.Parent = label
	label.Parent = gui
	gui.Parent = adornee

	local info = TweenInfo.new(0.8, Enum.EasingStyle.Quad, Enum.EasingDirection.Out)
	TweenService:Create(gui, info, { StudsOffset = Vector3.new(0, 6, 0) }):Play()
	TweenService:Create(label, info, { TextTransparency = 1 }):Play()
	TweenService:Create(stroke, info, { Transparency = 1 }):Play()
	task.delay(0.85, gui.Destroy, gui)
end
```

> Pool these on busy screens (pens with 20+ pets) instead of creating new instances every second.

## 3. Window pop open / quick close

```lua
local OPEN = TweenInfo.new(0.18, Enum.EasingStyle.Back, Enum.EasingDirection.Out)
local CLOSE = TweenInfo.new(0.12, Enum.EasingStyle.Quad, Enum.EasingDirection.In)

local function open(window: Frame)
	local s = window:FindFirstChildOfClass("UIScale") or Instance.new("UIScale", window)
	s.Scale = 0.8
	window.Visible = true
	TweenService:Create(s, OPEN, { Scale = 1 }):Play()
end

local function close(window: Frame)
	local s = window:FindFirstChildOfClass("UIScale")
	local t = TweenService:Create(s, CLOSE, { Scale = 0.85 })
	t.Completed:Once(function() window.Visible = false end)
	t:Play()
end
```

## 4. Shine sweep across a premium button

```lua
-- Button has a UIGradient named Shine with Transparency 1 → 0.4 → 1 and Rotation 20
local shine = button.Shine
local sweep = TweenService:Create(shine, TweenInfo.new(0.9, Enum.EasingStyle.Linear), { Offset = Vector2.new(1, 0) })
task.spawn(function()
	while button.Parent do
		shine.Offset = Vector2.new(-1, 0)
		sweep:Play()
		task.wait(3)
	end
end)
```

## 5. Camera shake on impact

```lua
local RunService = game:GetService("RunService")

local function shake(duration: number, magnitude: number)
	local camera = workspace.CurrentCamera
	local start = os.clock()
	local name = "Shake" .. tostring(start)
	RunService:BindToRenderStep(name, Enum.RenderPriority.Camera.Value + 1, function()
		local t = os.clock() - start
		if t >= duration then
			RunService:UnbindFromRenderStep(name)
			return
		end
		local fade = 1 - t / duration
		local offset = Vector3.new(math.noise(t * 25, 0), math.noise(0, t * 25), 0) * magnitude * fade
		camera.CFrame *= CFrame.new(offset)
	end)
end
-- shake(0.2, 0.4) on a bat hit; respect a "Reduce motion" setting
```

## 6. Burst of particles on reward

Keep a disabled `ParticleEmitter` (stars/confetti, Rate 0) on the player or the reward and call `emitter:Emit(30)`; scale the count with rarity (Common 10 → Secret 120).

## 7. Idle bob for pets/eggs

```lua
local function bob(model: Model)
	local base = model:GetPivot()
	local t0 = math.random() * 10
	return RunService.Heartbeat:Connect(function()
		local t = os.clock() + t0
		model:PivotTo(base * CFrame.new(0, math.sin(t * 2) * 0.25, 0) * CFrame.Angles(0, math.sin(t) * 0.1, 0))
	end)
end
```

(For many pets, animate on the client only and batch them in one Heartbeat loop.)

## 8. Sound rules

- Distinct sounds per rarity; ascending pitch for streaks/combos (`Sound.PlaybackSpeed = 1 + 0.05 * streak`).
- Randomise pitch ±5% on repeated sounds (coins) so they don't fatigue.
- Duck music (`SoundGroup.Volume`) during reveals.
