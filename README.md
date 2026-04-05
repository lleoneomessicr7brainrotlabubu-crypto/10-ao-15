-- [[ COELHO HUB - MODULE GORILLAS (10-15) ]]

local Players = game:GetService("Players")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Workspace = game:GetService("Workspace")
local player = Players.LocalPlayer
local CommF = ReplicatedStorage:WaitForChild("Remotes"):WaitForChild("CommF_")

-- 1. CONFIGURAÇÕES DOS GORILLAS
local Config = {
    QuestID = "JungleQuest",
    QuestIndex = 2, -- 2 seleciona Gorillas
    TargetName = "Gorilla",
    SpawnPoint = CFrame.new(-1214, 28, -25), -- Localização dos Gorillas
    AttackDistance = 65
}

-- 2. SEU SISTEMA DE ATAQUE NATIVO (INTEGRADO)
local function SuperAttack()
    local char = player.Character
    if not char or not char:FindFirstChildOfClass("Tool") then return end

    local targets = {}
    for _, v in pairs(Workspace.Enemies:GetChildren()) do
        -- Filtra apenas os Gorillas para não bater em nada errado
        if v.Name == Config.TargetName and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
            local dist = (v.HumanoidRootPart.Position - char.HumanoidRootPart.Position).Magnitude
            if dist < Config.AttackDistance then
                table.insert(targets, v)
            end
        end
    end

    if #targets > 0 then
        local net = ReplicatedStorage:WaitForChild("Modules"):WaitForChild("Net")
        
        -- Bypass de Registro e Hit Massivo (O código que você mandou)
        net["RE/RegisterAttack"]:FireServer(0)
        
        local args = {nil, {}}
        for i, v in pairs(targets) do
            if not args[1] then args[1] = v.Head end
            args[2][i] = {v, v.HumanoidRootPart}
        end
        net["RE/RegisterHit"]:FireServer(unpack(args))
    end
end

-- 3. BRING MOB (PUXA GORILLAS PARA O PERSONAGEM)
local function BringGorillas()
    for _, v in pairs(Workspace.Enemies:GetChildren()) do
        if v.Name == Config.TargetName and v:FindFirstChild("HumanoidRootPart") then
            -- Puxa o Gorilla exatamente para a sua posição
            v.HumanoidRootPart.CFrame = player.Character.HumanoidRootPart.CFrame
            v.HumanoidRootPart.CanCollide = false
            if v:FindFirstChild("Humanoid") then
                v.Humanoid.WalkSpeed = 0
            end
        end
    end
end

-- 4. LOOP DE EXECUÇÃO (MISSÃO + ATAQUE + MOVIMENTAÇÃO)
spawn(function()
    print("Coelho Hub: Farm de Gorillas (10-15) Ativado! 🦍")
    
    while true do
        local level = player.Data.Level.Value
        
        -- Condição de Parada: Nível 15
        if level >= 15 then 
            print("Coelho Hub: Meta atingida! Pronto para o próximo nível.")
            break 
        end

        pcall(function()
            -- LÓGICA DE MISSÃO (StartQuest)
            if player.Data.Quest.Value == "" then
                CommF:InvokeServer("StartQuest", Config.QuestID, Config.QuestIndex)
            end

            -- TELEPORTE PARA O SPAWN (Se estiver longe da área dos Gorillas)
            local dist = (player.Character.HumanoidRootPart.Position - Config.SpawnPoint.Position).Magnitude
            if dist > 50 then
                player.Character.HumanoidRootPart.CFrame = Config.SpawnPoint
            end

            -- EXECUÇÃO DO ATAQUE POTENTE
            BringGorillas()
            SuperAttack()
        end)
        
        task.wait(0.1) -- Velocidade do Fast Attack
    end
end)
-- [[ COELHO HUB - MODULE GORILLAS (10-15) ]]

local Players = game:GetService("Players")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Workspace = game:GetService("Workspace")
local player = Players.LocalPlayer
local CommF = ReplicatedStorage:WaitForChild("Remotes"):WaitForChild("CommF_")

-- 1. CONFIGURAÇÕES DOS GORILLAS
local Config = {
    QuestID = "JungleQuest",
    QuestIndex = 2, -- 2 seleciona Gorillas
    TargetName = "Gorilla",
    SpawnPoint = CFrame.new(-1214, 28, -25), -- Localização dos Gorillas
    AttackDistance = 65
}

-- 2. SEU SISTEMA DE ATAQUE NATIVO (INTEGRADO)
local function SuperAttack()
    local char = player.Character
    if not char or not char:FindFirstChildOfClass("Tool") then return end

    local targets = {}
    for _, v in pairs(Workspace.Enemies:GetChildren()) do
        -- Filtra apenas os Gorillas para não bater em nada errado
        if v.Name == Config.TargetName and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
            local dist = (v.HumanoidRootPart.Position - char.HumanoidRootPart.Position).Magnitude
            if dist < Config.AttackDistance then
                table.insert(targets, v)
            end
        end
    end

    if #targets > 0 then
        local net = ReplicatedStorage:WaitForChild("Modules"):WaitForChild("Net")
        
        -- Bypass de Registro e Hit Massivo (O código que você mandou)
        net["RE/RegisterAttack"]:FireServer(0)
        
        local args = {nil, {}}
        for i, v in pairs(targets) do
            if not args[1] then args[1] = v.Head end
            args[2][i] = {v, v.HumanoidRootPart}
        end
        net["RE/RegisterHit"]:FireServer(unpack(args))
    end
end

-- 3. BRING MOB (PUXA GORILLAS PARA O PERSONAGEM)
local function BringGorillas()
    for _, v in pairs(Workspace.Enemies:GetChildren()) do
        if v.Name == Config.TargetName and v:FindFirstChild("HumanoidRootPart") then
            -- Puxa o Gorilla exatamente para a sua posição
            v.HumanoidRootPart.CFrame = player.Character.HumanoidRootPart.CFrame
            v.HumanoidRootPart.CanCollide = false
            if v:FindFirstChild("Humanoid") then
                v.Humanoid.WalkSpeed = 0
            end
        end
    end
end

-- 4. LOOP DE EXECUÇÃO (MISSÃO + ATAQUE + MOVIMENTAÇÃO)
spawn(function()
    print("Coelho Hub: Farm de Gorillas (10-15) Ativado! 🦍")
    
    while true do
        local level = player.Data.Level.Value
        
        -- Condição de Parada: Nível 15
        if level >= 15 then 
            print("Coelho Hub: Meta atingida! Pronto para o próximo nível.")
            break 
        end

        pcall(function()
            -- LÓGICA DE MISSÃO (StartQuest)
            if player.Data.Quest.Value == "" then
                CommF:InvokeServer("StartQuest", Config.QuestID, Config.QuestIndex)
            end

            -- TELEPORTE PARA O SPAWN (Se estiver longe da área dos Gorillas)
            local dist = (player.Character.HumanoidRootPart.Position - Config.SpawnPoint.Position).Magnitude
            if dist > 50 then
                player.Character.HumanoidRootPart.CFrame = Config.SpawnPoint
            end

            -- EXECUÇÃO DO ATAQUE POTENTE
            BringGorillas()
            SuperAttack()
        end)
        
        task.wait(0.1) -- Velocidade do Fast Attack
    end
end)

print("Coelho Hub: Módulo 10-15 Carregado com Sucesso! 🕶️🔥🐇")
print("Coelho Hub: Módulo 10-15 Carregado com Sucesso! 🕶️🔥🐇")
