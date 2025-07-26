-- Vox Seas Auto Fruit TP + Auto Farm NPCs
-- Use com KRNL, Fluxus ou Synapse X

local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local VirtualInputManager = game:GetService("VirtualInputManager")
local player = Players.LocalPlayer

-- Função para atacar (simula clique do mouse)
function attack()
    VirtualInputManager:SendMouseButtonEvent(0, 0, 0, true, game, 0)
    VirtualInputManager:SendMouseButtonEvent(0, 0, 0, false, game, 0)
end

-- Auto Teleport para frutas
spawn(function()
    while task.wait(1) do
        for _, obj in pairs(workspace:GetDescendants()) do
            if obj:IsA("Tool") and obj:FindFirstChild("Handle") and string.find(string.lower(obj.Name), "fruit") then
                if player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
                    player.Character.HumanoidRootPart.CFrame = obj.Handle.CFrame + Vector3.new(0, 3, 0)
                    wait(1)
                end
            end
        end
    end
end)

-- Auto Farm de NPCs
spawn(function()
    while task.wait(1) do
        for _, npc in pairs(workspace:GetDescendants()) do
            if npc:IsA("Model") and npc:FindFirstChild("Humanoid") and npc:FindFirstChild("HumanoidRootPart") then
                if npc.Humanoid.Health > 0 and npc.Name ~= player.Name then
                    local char = player.Character
                    if char and char:FindFirstChild("HumanoidRootPart") then
                        char.HumanoidRootPart.CFrame = npc.HumanoidRootPart.CFrame + Vector3.new(0, 5, 0)
                        attack()
                        wait(0.5)
                    end
                end
            end
        end
    end
end)
