# Application-for-hidden-devs
```lua
local ui = script.Parent

local RS = game:GetService("RunService")

local clicked = false

local player = game.Players.LocalPlayer

local mouse = player:GetMouse()

local UID = game:GetService("UserInputService")

local cam = workspace.CurrentCamera

ui.MouseButton1Click:Connect(function()
	if clicked == false then
		clicked = true
		player.Character:FindFirstChild("Humanoid").WalkSpeed = 0
		player.Character:FindFirstChild("Humanoid").JumpHeight = 0
		local clone = game.ReplicatedStorage.Wall:Clone()
		clone.Parent = workspace
		clone.Transparency = .3
		clone.BrickColor = BrickColor.new("Forest green")
		cam.CameraType = "Scriptable"
		cam:Interpolate(game.Workspace.CamPart.CFrame,game.Workspace.SpawnLocation.CFrame, .5)
		local placing = true
			
		RS.RenderStepped:Connect(function()
			if placing == true then
				clone.Position = Vector3.new(mouse.Hit.X,9.216, mouse.Hit.Z)
			end
		end)
			
		UID.InputBegan:Connect(function(input, gameProcessedEvent)
			if input.UserInputType == Enum.UserInputType.MouseButton1 then
				placing = false
				clone.Position = Vector3.new(mouse.Hit.X,9.216, mouse.Hit.Z)
				clone.BrickColor = BrickColor.new("Medium Stone Grey")
				clone.Transparency = 0
				player.Character:FindFirstChild("Humanoid").WalkSpeed = 16
				player.Character:FindFirstChild("Humanoid").JumpHeight = 7.2
				cam.CameraType = "Custom"
			end
		end)	
	end
end)
```
