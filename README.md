-- Configurações do ESP
local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer

-- Função para desenhar o ESP
local function createESP(player)
    local espBox = Instance.new("BoxHandleAdornment")
    espBox.Size = Vector3.new(4, 6, 2)  -- Tamanho do box
    espBox.Color3 = player.TeamColor == LocalPlayer.TeamColor and Color3.new(1, 1, 1) or Color3.new(1, 0, 0)  -- Branco para aliados, vermelho para inimigos
    espBox.AlwaysOnTop = true
    espBox.ZIndex = 10
    espBox.Adornee = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
    espBox.Parent = game.Workspace

    local espLine = Instance.new("LineHandleAdornment")
    espLine.Length = 10
    espLine.Color3 = espBox.Color3
    espLine.AlwaysOnTop = true
    espLine.ZIndex = 10
    espLine.Adornee = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
    espLine.Parent = game.Workspace
end

-- Monitorar os jogadores
Players.PlayerAdded:Connect(function(player)
    player.CharacterAdded:Connect(function()
        createESP(player)
    end)
end)

-- Criar ESP para jogadores já existentes
for _, player in ipairs(Players:GetPlayers()) do
    if player ~= LocalPlayer then
        createESP(player)
    end
end
