local UIS = game:GetService("UserInputService")
local Player = game.Players.LocalPlayer
local Character = Player.Character
local Humanoid = Character:WaitForChild("Humanoid" ,5)
local StaminaUsed = script:WaitForChild("StaminaUsed" ,5)

local Keybind = "LeftShift"
local MaxStamina = 100
local NormalWalkspeed = 16
local SprintWalkspeed = 32

local StaminaCount = MaxStamina

UIS.InputBegan:Connect(function(key, processed)
	if key.UserInputType == Enum.UserInputType.Keyboard then
		if key.KeyCode == Enum.KeyCode[Keybind] and StaminaCount > 0 then
			StaminaUsed.Value = true
		end
	end
end)

UIS.InputEnded:Connect(function(key, processed)
	if key.UserInputType == Enum.UserInputType.Keyboard then
		if key.KeyCode == Enum.KeyCode[Keybind] then
			StaminaUsed.Value = false
		end
	end
end)

StaminaUsed.Changed:Connect(function()
	if StaminaUsed.Value == true then
		Humanoid.WalkSpeed = SprintWalkspeed
		repeat
			wait(0.1)
			if StaminaCount > 0 then
				StaminaCount = StaminaCount - 1
				script.Parent.Frame.Size = UDim2.new(StaminaCount / MaxStamina, 0, 1, 0)
				script.Parent.Info.Text = StaminaCount.. "/" ..MaxStamina
			end
		until
		StaminaCount <= 0 or StaminaUsed.Value == false
		Humanoid.WalkSpeed = NormalWalkspeed
	elseif StaminaUsed.Value == false then
		Humanoid.WalkSpeed = NormalWalkspeed
		repeat
			wait(0.1)
			if StaminaCount < MaxStamina then
				StaminaCount = StaminaCount + 1
				script.Parent.Frame.Size = UDim2.new(StaminaCount / MaxStamina, 0, 1, 0)
				script.Parent.Info.Text = StaminaCount.. "/" ..MaxStamina
			end
		until
		StaminaCount == MaxStamina or StaminaUsed.Value == true
	end
end)

Made By Me
