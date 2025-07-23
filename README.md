--[[
    Dudu Hub - Blox Fruits Script v1.9
    - Visual dark, animado, key system ("duduhubv1")
    - 3 tentativas para digitar a key correta, senão mostra link do Discord!
    - Teleporte corrigido e estável: não volta para posição antiga.
    - Funções completas e ESP Players com highlight vermelho.
]]

local DuduHub = Instance.new("ScreenGui")
local Main = Instance.new("Frame")
local Title = Instance.new("TextLabel")
local AutoFarmLevelBtn = Instance.new("TextButton")
local AutoStatsBtn = Instance.new("TextButton")
local TeleportBtn = Instance.new("TextButton")
local EspFrutaBtn = Instance.new("TextButton")
local EspBtn = Instance.new("TextButton")
local MinimizeBtn = Instance.new("TextButton")
local KeyFrame = Instance.new("Frame")
local KeyLabel = Instance.new("TextLabel")
local KeyBox = Instance.new("TextBox")
local KeyBtn = Instance.new("TextButton")
local TeleportMenu = Instance.new("Frame")
local DiscordFrame = Instance.new("Frame")
local DiscordLabel = Instance.new("TextLabel")
local DiscordBtn = Instance.new("TextButton")

DuduHub.Name = "DuduHub"
DuduHub.Parent = game.CoreGui

Main.Name = "Main"
Main.Parent = DuduHub
Main.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
Main.BackgroundTransparency = 0.7
Main.Position = UDim2.new(0.5, -150, 0.5, -175)
Main.Size = UDim2.new(0, 0, 0, 0)
Main.Active = true
Main.Draggable = true

Title.Name = "Title"
Title.Parent = Main
Title.BackgroundTransparency = 1
Title.Position = UDim2.new(0, 0, 0, 0)
Title.Size = UDim2.new(1, 0, 0, 50)
Title.Font = Enum.Font.GothamBold
Title.Text = "Dudu Hub - Blox Fruits"
Title.TextColor3 = Color3.fromRGB(255, 255, 255)
Title.TextSize = 28

MinimizeBtn.Parent = Main
MinimizeBtn.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
MinimizeBtn.Position = UDim2.new(0.88, 0, 0.05, 0)
MinimizeBtn.Size = UDim2.new(0, 30, 0, 30)
MinimizeBtn.Font = Enum.Font.GothamBold
MinimizeBtn.Text = "_"
MinimizeBtn.TextColor3 = Color3.fromRGB(255,255,255)
MinimizeBtn.TextSize = 22
MinimizeBtn.Name = "MinimizeBtn"

local buttons = {
    {AutoFarmLevelBtn, "Auto Farm Level"},
    {AutoStatsBtn, "Auto Stats"},
    {TeleportBtn, "Teleport"},
    {EspFrutaBtn, "ESP Fruta"},
    {EspBtn, "ESP Players"},
}

for i, btn in ipairs(buttons) do
    local Button, Text = btn[1], btn[2]
    Button.Parent = Main
    Button.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
    Button.BackgroundTransparency = 0.4
    Button.Position = UDim2.new(0.1, 0, 0, 60 + ((i-1)*55))
    Button.Size = UDim2.new(0.8, 0, 0, 40)
    Button.Font = Enum.Font.Gotham
    Button.Text = Text
    Button.TextColor3 = Color3.fromRGB(255,255,255)
    Button.TextSize = 20
    Button.Visible = false
end

Title.Visible = false
MinimizeBtn.Visible = false

-- Minimizar função
local minimized = false
MinimizeBtn.MouseButton1Click:Connect(function()
    minimized = not minimized
    for i, btn in ipairs(buttons) do
        btn[1].Visible = (not minimized and KeyFrame.Visible == false and not DiscordFrame.Visible)
    end
    Title.Visible = not minimized
    if minimized then
        Main.Size = UDim2.new(0, 70, 0, 50)
        MinimizeBtn.Position = UDim2.new(0.08, 0, 0.2, 0)
    else
        Main.Size = UDim2.new(0, 300, 0, 350)
        MinimizeBtn.Position = UDim2.new(0.88, 0, 0.05, 0)
    end
end)

-- Key System (painel)
KeyFrame.Name = "KeyFrame"
KeyFrame.Parent = Main
KeyFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
KeyFrame.BackgroundTransparency = 0.4
KeyFrame.Position = UDim2.new(0,0,0,0)
KeyFrame.Size = UDim2.new(1,0,1,0)

KeyLabel.Name = "KeyLabel"
KeyLabel.Parent = KeyFrame
KeyLabel.BackgroundTransparency = 1
KeyLabel.Position = UDim2.new(0, 0, 0, 40)
KeyLabel.Size = UDim2.new(1, 0, 0, 40)
KeyLabel.Font = Enum.Font.GothamBold
KeyLabel.Text = "Digite a Key para liberar o script"
KeyLabel.TextColor3 = Color3.fromRGB(255,255,255)
KeyLabel.TextSize = 20

KeyBox.Name = "KeyBox"
KeyBox.Parent = KeyFrame
KeyBox.BackgroundColor3 = Color3.fromRGB(50,50,50)
KeyBox.BackgroundTransparency = 0.2
KeyBox.Position = UDim2.new(0.1,0,0,100)
KeyBox.Size = UDim2.new(0.8,0,0,40)
KeyBox.Font = Enum.Font.Gotham
KeyBox.Text = ""
KeyBox.TextColor3 = Color3.fromRGB(255,255,255)
KeyBox.TextSize = 18
KeyBox.PlaceholderText = "Insira a Key..."

KeyBtn.Name = "KeyBtn"
KeyBtn.Parent = KeyFrame
KeyBtn.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
KeyBtn.Position = UDim2.new(0.1, 0, 0, 160)
KeyBtn.Size = UDim2.new(0.8, 0, 0, 40)
KeyBtn.Font = Enum.Font.GothamBold
KeyBtn.Text = "Liberar"
KeyBtn.TextColor3 = Color3.fromRGB(255,255,255)
KeyBtn.TextSize = 20

-- Discord Frame
DiscordFrame.Name = "DiscordFrame"
DiscordFrame.Parent = Main
DiscordFrame.BackgroundColor3 = Color3.fromRGB(30, 0, 0)
DiscordFrame.BackgroundTransparency = 0.3
DiscordFrame.Size = UDim2.new(1,0,1,0)
DiscordFrame.Position = UDim2.new(0,0,0,0)
DiscordFrame.Visible = false

DiscordLabel.Name = "DiscordLabel"
DiscordLabel.Parent = DiscordFrame
DiscordLabel.BackgroundTransparency = 1
DiscordLabel.Position = UDim2.new(0, 0, 0, 40)
DiscordLabel.Size = UDim2.new(1, 0, 0, 60)
DiscordLabel.Font = Enum.Font.GothamBold
DiscordLabel.Text = "Você errou a key 3 vezes!\nAcesse o nosso Discord:"
DiscordLabel.TextColor3 = Color3.fromRGB(255,80,80)
DiscordLabel.TextSize = 18

DiscordBtn.Name = "DiscordBtn"
DiscordBtn.Parent = DiscordFrame
DiscordBtn.BackgroundColor3 = Color3.fromRGB(80,0,0)
DiscordBtn.Position = UDim2.new(0.1, 0, 0, 120)
DiscordBtn.Size = UDim2.new(0.8, 0, 0, 40)
DiscordBtn.Font = Enum.Font.GothamBold
DiscordBtn.Text = "https://discord.gg/rkB256SM"
DiscordBtn.TextColor3 = Color3.fromRGB(255,255,255)
DiscordBtn.TextSize = 20
DiscordBtn.MouseButton1Click:Connect(function()
    setclipboard("https://discord.gg/rkB256SM")
    DiscordBtn.Text = "Link copiado!"
    wait(2)
    DiscordBtn.Text = "https://discord.gg/rkB256SM"
end)

local keyAttempts = 0
local function LiberarScript()
    if KeyBox.Text == "duduhubv1" then
        KeyLabel.Text = "Key correta!"
        wait(0.5)
        KeyFrame.Visible = false
        for i, btn in ipairs(buttons) do btn[1].Visible = true end
        Title.Visible = true
        MinimizeBtn.Visible = true
    else
        keyAttempts = keyAttempts + 1
        if keyAttempts >= 3 then
            KeyFrame.Visible = false
            DiscordFrame.Visible = true
            Title.Visible = false
            for i, btn in ipairs(buttons) do btn[1].Visible = false end
        else
            KeyLabel.Text = "Key incorreta! Tentativa " .. keyAttempts .. " de 3"
        end
    end
end
KeyBtn.MouseButton1Click:Connect(LiberarScript)
KeyBox.FocusLost:Connect(function(enter) if enter then LiberarScript() end end)

-- Animação de entrada
Main.Visible = true
KeyFrame.Visible = true
DiscordFrame.Visible = false
Main.Size = UDim2.new(0, 0, 0, 0)
Main.Position = UDim2.new(0.5, -0, 0.5, -0)
wait(0.1)
local TweenService = game:GetService("TweenService")
local tween = TweenService:Create(Main, TweenInfo.new(0.6, Enum.EasingStyle.Back, Enum.EasingDirection.Out), {Size = UDim2.new(0, 300, 0, 350), Position = UDim2.new(0.5, -150, 0.5, -175)})
tween:Play()

-- AUTO FARM LEVEL (exemplo simples)
local autoFarmOn = false
AutoFarmLevelBtn.MouseButton1Click:Connect(function()
    autoFarmOn = not autoFarmOn
    if autoFarmOn then
        AutoFarmLevelBtn.Text = "Auto Farm Level [ON]"
        print("[Dudu Hub] Auto Farm Level ativado!")
        spawn(function()
            while autoFarmOn do
                local player = game.Players.LocalPlayer
                local hrp = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
                if hrp then
                    hrp.CFrame = CFrame.new(1060, 16, 1547)
                    wait(1)
                    local npc = workspace:FindFirstChild("BanditQuestGiver")
                    if npc then
                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("StartQuest", "BanditQuest", 1)
                        wait(.5)
                    end
                    local mob = workspace:FindFirstChild("Bandit")
                    if mob and mob:FindFirstChild("HumanoidRootPart") then
                        hrp.CFrame = mob.HumanoidRootPart.CFrame + Vector3.new(0,2,0)
                        wait(.2)
                        player.Character:FindFirstChildOfClass("Tool"):Activate()
                        wait(1)
                    else
                        wait(1)
                    end
                end
            end
        end)
    else
        AutoFarmLevelBtn.Text = "Auto Farm Level"
        print("[Dudu Hub] Auto Farm Level desativado!")
    end
end)

-- AUTO STATS (distribui pontos automaticamente)
local autoStatsOn = false
AutoStatsBtn.MouseButton1Click:Connect(function()
    autoStatsOn = not autoStatsOn
    if autoStatsOn then
        AutoStatsBtn.Text = "Auto Stats [ON]"
        print("[Dudu Hub] Auto Stats ativado!")
        spawn(function()
            while autoStatsOn do
                local Replicated = game:GetService("ReplicatedStorage")
                local CommF = Replicated:WaitForChild("Remotes"):WaitForChild("CommF_")
                for _, stat in ipairs({"Melee","Defense","Sword","Gun"}) do
                    CommF:InvokeServer("AddPoint", stat, 10)
                    wait(.1)
                end
                wait(5)
            end
        end)
    else
        AutoStatsBtn.Text = "Auto Stats"
        print("[Dudu Hub] Auto Stats desativado!")
    end
end)

-- TELEPORTE ESTÁVEL (NÃO VOLTA PRA POSIÇÃO ANTIGA)
local function StableTeleport(targetPosition)
    local player = game.Players.LocalPlayer
    local char = player.Character or player.CharacterAdded:Wait()
    local hrp = char:FindFirstChild("HumanoidRootPart") or char:WaitForChild("HumanoidRootPart")

    -- Desabilita temporariamente a física e move todos os parts
    for _,v in pairs(char:GetChildren()) do
        if v:IsA("BasePart") then
            v.Anchored = true
        end
    end

    char:SetPrimaryPartCFrame(CFrame.new(targetPosition))
    wait(0.2)

    for _,v in pairs(char:GetChildren()) do
        if v:IsA("BasePart") then
            v.Anchored = false
        end
    end
end

TeleportMenu.Name = "TeleportMenu"
TeleportMenu.Parent = Main
TeleportMenu.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
TeleportMenu.BackgroundTransparency = 0.6
TeleportMenu.Position = UDim2.new(0.2,0,0.2,0)
TeleportMenu.Size = UDim2.new(0,200,0,250)
TeleportMenu.Visible = false

local ilhas = {
    {"Starter Island", Vector3.new(1060, 16, 1547)},
    {"Pirate Village", Vector3.new(-1100, 13, 3827)},
    {"Jungle", Vector3.new(-1600, 12, 1650)},
    {"Desert", Vector3.new(1094, 16, 4288)},
    {"Middle Town", Vector3.new(-555, 8, 3820)},
}

for i, ilha in ipairs(ilhas) do
    local btn = Instance.new("TextButton")
    btn.Parent = TeleportMenu
    btn.BackgroundColor3 = Color3.fromRGB(30,30,30)
    btn.BackgroundTransparency = 0.2
    btn.Position = UDim2.new(0,10,0,10+(i-1)*45)
    btn.Size = UDim2.new(0,180,0,40)
    btn.Font = Enum.Font.Gotham
    btn.Text = ilha[1]
    btn.TextColor3 = Color3.fromRGB(255,255,255)
    btn.TextSize = 18

    btn.MouseButton1Click:Connect(function()
        StableTeleport(ilha[2])
        TeleportMenu.Visible = false
    end)
end

TeleportBtn.MouseButton1Click:Connect(function()
    TeleportMenu.Visible = not TeleportMenu.Visible
end)

-- ESP FRUTA funcional
local frutaEspAtivo = false
local frutaEspBoxes = {}

local function clearFrutaEsp()
    for _,v in pairs(frutaEspBoxes) do
        if v and v.Parent then
            v:Destroy()
        end
    end
    frutaEspBoxes = {}
end

local function espFruta()
    clearFrutaEsp()
    for _, obj in pairs(workspace:GetChildren()) do
        if obj:IsA("Tool") and obj.Parent == workspace then
            local box = Instance.new("BoxHandleAdornment")
            box.Size = Vector3.new(2,2,2)
            box.Color3 = Color3.fromRGB(255,0,0)
            box.Transparency = 0.5
            box.AdornedPart = obj:FindFirstChild("Handle")
            box.Parent = obj
            box.AlwaysOnTop = true
            table.insert(frutaEspBoxes, box)
        end
    end
end

EspFrutaBtn.MouseButton1Click:Connect(function()
    frutaEspAtivo = not frutaEspAtivo
    if frutaEspAtivo then
        EspFrutaBtn.Text = "ESP Fruta [ON]"
        print("[Dudu Hub] ESP Fruta ativado!")
        espFruta()
        frutaEspBoxes._connection = workspace.ChildAdded:Connect(function(obj)
            if frutaEspAtivo then
                espFruta()
            end
        end)
    else
        EspFrutaBtn.Text = "ESP Fruta"
        print("[Dudu Hub] ESP Fruta desativado!")
        clearFrutaEsp()
        if frutaEspBoxes._connection then
            frutaEspBoxes._connection:Disconnect()
            frutaEspBoxes._connection = nil
        end
    end
end)

-- ESP PLAYERS funcional COM HIGHLIGHT VERMELHO
local espPlayersOn = false
local playerEspBoxes = {}
local playerHighlights = {}

local function clearPlayerEsp()
    for _,v in pairs(playerEspBoxes) do
        if v and v.Parent then
            v:Destroy()
        end
    end
    playerEspBoxes = {}
    for _,v in pairs(playerHighlights) do
        if v and v.Parent then
            v:Destroy()
        end
    end
    playerHighlights = {}
end

local function espPlayers()
    clearPlayerEsp()
    for _,plr in pairs(game.Players:GetPlayers()) do
        if plr ~= game.Players.LocalPlayer and plr.Character and plr.Character:FindFirstChild("HumanoidRootPart") then
            local box = Instance.new("BoxHandleAdornment")
            box.Size = Vector3.new(3,6,3)
            box.Color3 = Color3.fromRGB(255,0,0)
            box.Transparency = 0.1
            box.AdornedPart = plr.Character.HumanoidRootPart
            box.Parent = plr.Character
            box.AlwaysOnTop = true
            table.insert(playerEspBoxes, box)
            -- Highlight vermelho
            local highlight = Instance.new("Highlight")
            highlight.FillColor = Color3.fromRGB(255,0,0)
            highlight.FillTransparency = 0.4
            highlight.OutlineColor = Color3.fromRGB(255,0,0)
            highlight.OutlineTransparency = 0
            highlight.Adornee = plr.Character
            highlight.DepthMode = Enum.HighlightDepthMode.AlwaysOnTop
            highlight.Parent = plr.Character
            table.insert(playerHighlights, highlight)
        end
    end
end

EspBtn.MouseButton1Click:Connect(function()
    espPlayersOn = not espPlayersOn
    if espPlayersOn then
        EspBtn.Text = "ESP Players [ON]"
        print("[Dudu Hub] ESP Players ativado!")
        espPlayers()
        playerEspBoxes._connection = game.Players.PlayerAdded:Connect(function(p)
            p.CharacterAdded:Connect(function()
                if espPlayersOn then
                    espPlayers()
                end
            end)
        end)
        game.Players.PlayerRemoving:Connect(function()
            if espPlayersOn then
                espPlayers()
            end
        end)
    else
        EspBtn.Text = "ESP Players"
        print("[Dudu Hub] ESP Players desativado!")
        clearPlayerEsp()
        if playerEspBoxes._connection then
            playerEspBoxes._connection:Disconnect()
            playerEspBoxes._connection = nil
        end
    end
end)

print("[Dudu Hub] Carregado com sucesso! Insira a Key para liberar as funções.")
