local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Players = game:GetService("Players")
local UserInputService = game:GetService("UserInputService")

local armaNome = ".38" -- Substitua pelo nome da arma no ReplicatedStorage
local teclaAtivacao = Enum.KeyCode.G -- Tecla para pegar a arma (pode mudar)

local function darArma()
    local player = Players.LocalPlayer
    local character = player.Character or player.CharacterAdded:Wait()
    local backpack = player:FindFirstChild("Backpack")

    if backpack then
        local arma = ReplicatedStorage:FindFirstChild(armaNome)
        if arma then
            local armaClone = arma:Clone()
            armaClone.Parent = backpack
            character.Humanoid:EquipTool(armaClone) -- Equipa automaticamente
        else
            warn("A arma '" .. armaNome .. "' não foi encontrada no ReplicatedStorage!")
        end
    end
end

UserInputService.InputBegan:Connect(function(input, gameProcessed)
    if not gameProcessed and input.KeyCode == teclaAtivacao then
        darArma()
    end
end)
