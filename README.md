local Players = game:GetService("Players")
local player = Players.LocalPlayer

-- Criar a GUI
local screenGui = Instance.new("ScreenGui", player:WaitForChild("PlayerGui"))
screenGui.Name = "mglHubGui"

-- Texto temporário grande na tela
local tempLabel = Instance.new("TextLabel")
tempLabel.Size = UDim2.new(1, 0, 0.2, 0)
tempLabel.Position = UDim2.new(0, 0, 0.4, 0)
tempLabel.BackgroundTransparency = 1
tempLabel.Text = "{mglHub}"
tempLabel.TextColor3 = Color3.new(1, 1, 1)
tempLabel.Font = Enum.Font.SourceSansBold
tempLabel.TextSize = 60
tempLabel.TextStrokeTransparency = 0
tempLabel.TextStrokeColor3 = Color3.new(0, 0, 0)
tempLabel.Parent = screenGui

task.delay(3, function()
	if tempLabel then
		tempLabel:Destroy()
	end
end)

-- Função para criar botões
local function createButton(text, position)
	local button = Instance.new("TextButton")
	button.Size = UDim2.new(0, 150, 0, 40)
	button.Position = position
	button.Text = text
	button.BackgroundColor3 = Color3.new(0.2, 0.6, 1)
	button.TextColor3 = Color3.new(1, 1, 1)
	button.Font = Enum.Font.SourceSansBold
	button.TextSize = 20
	button.Parent = screenGui
	return button
end

-- Botão Spawnar Bloco
local spawnBlockButton = createButton("Spawnar Bloco", UDim2.new(0, 20, 0, 100))
spawnBlockButton.MouseButton1Click:Connect(function()
	local char = player.Character or player.CharacterAdded:Wait()
	local root = char:WaitForChild("HumanoidRootPart")

	local part = Instance.new("Part")
	part.Size = Vector3.new(3, 3, 3)
	part.Position = root.Position - Vector3.new(0, 3, 0)
	part.Anchored = true
	part.Color = Color3.new(1, 0, 0)
	part.Name = "BlocoSpawnado"
	part.Parent = workspace
end)

-- Botão Invisível
local invisibleButton = createButton("Invisível", UDim2.new(0, 20, 0, 150))
invisibleButton.MouseButton1Click:Connect(function()
	local char = player.Character or player.CharacterAdded:Wait()
	for _, part in ipairs(char:GetDescendants()) do
		if part:IsA("BasePart") and part.Name ~= "HumanoidRootPart" then
			part.Transparency = 1
		elseif part:IsA("Decal") then
			part.Transparency = 1
		end
	end
end)
