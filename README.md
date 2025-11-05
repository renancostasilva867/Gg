-- Criar GUI principal
local player = game.Players.LocalPlayer
local gui = Instance.new("ScreenGui", player:WaitForChild("PlayerGui"))
gui.Name = "HitboxMenu"

local frame = Instance.new("Frame", gui)
frame.Size = UDim2.new(0, 180, 0, 120)
frame.Position = UDim2.new(0.05, 0, 0.3, 0)
frame.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
frame.BackgroundTransparency = 0.5
frame.Active = true
frame.Draggable = true
frame.BorderSizePixel = 0

-- Título com efeito RGB
local title = Instance.new("TextLabel", frame)
title.Size = UDim2.new(1, 0, 0, 25)
title.Position = UDim2.new(0, 0, 0, 0)
title.Text = "Tiktok: @rennxzthegoat"
title.Font = Enum.Font.GothamBold
title.TextSize = 14
title.BackgroundTransparency = 1
title.TextStrokeTransparency = 0.5

-- Efeito RGB animado
task.spawn(function()
	while true do
		for i = 0, 255, 5 do
			title.TextColor3 = Color3.fromHSV(i/255, 1, 1)
			task.wait(0.05)
		end
	end
end)

-- Botão Remover Hitbox
local removeBtn = Instance.new("TextButton", frame)
removeBtn.Size = UDim2.new(0.9, 0, 0, 35)
removeBtn.Position = UDim2.new(0.05, 0, 0.3, 0)
removeBtn.Text = "Remover Hitbox"
removeBtn.Font = Enum.Font.GothamBold
removeBtn.TextSize = 14
removeBtn.BackgroundColor3 = Color3.fromRGB(255, 80, 80)
removeBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
removeBtn.BorderSizePixel = 0
removeBtn.AutoButtonColor = true
removeBtn.ZIndex = 2

-- Botão Desativar
local restoreBtn = Instance.new("TextButton", frame)
restoreBtn.Size = UDim2.new(0.9, 0, 0, 35)
restoreBtn.Position = UDim2.new(0.05, 0, 0.7, 0)
restoreBtn.Text = "Desativar"
restoreBtn.Font = Enum.Font.GothamBold
restoreBtn.TextSize = 14
restoreBtn.BackgroundColor3 = Color3.fromRGB(80, 255, 80)
restoreBtn.TextColor3 = Color3.fromRGB(0, 0, 0)
restoreBtn.BorderSizePixel = 0
restoreBtn.AutoButtonColor = true
restoreBtn.ZIndex = 2

-- Variáveis e funções
local character = player.Character or player.CharacterAdded:Wait()
local humanoid = character:WaitForChild("Humanoid")
local originalTransparency = {}

-- Função remover hitbox
removeBtn.MouseButton1Click:Connect(function()
	for _, part in pairs(character:GetDescendants()) do
		if part:IsA("BasePart") then
			originalTransparency[part] = part.Transparency
			part.Transparency = 1
			part.CanCollide = false
		end
	end
	humanoid.NameDisplayDistance = 0
end)

-- Função restaurar
restoreBtn.MouseButton1Click:Connect(function()
	for part, transparency in pairs(originalTransparency) do
		if part and part:IsA("BasePart") then
			part.Transparency = transparency
			part.CanCollide = true
		end
	end
	humanoid.NameDisplayDistance = 100
end)
