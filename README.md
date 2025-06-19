-- Painel Preto Moderno: KEY, VELOCIDADE, ESP, ATRAVESSAR PAREDE, GRUDAR MIRA, FLY (mobile/setas), INVISIBILIDADE
-- Feito por XLZIN (versão aprimorada, fly sem subir/ descer sozinho, funções mantidas após respawn, grudar mira ativável)
-- MODIFICADO: Todos os inimigos ficam vermelhos (Highlight vermelho) independente da distância

local KEY_CORRETA = "sxTKQP365"
local player = game.Players.LocalPlayer

-- GUI principal
local gui = Instance.new("ScreenGui")
gui.Name = "PainelXLZIN"
gui.Parent = game:GetService("CoreGui")
gui.ResetOnSpawn = false

-- Painel de Key (preto, arredondado)
local keyPanel = Instance.new("Frame")
keyPanel.Name = "KeyPanel"
keyPanel.Size = UDim2.new(0, 340, 0, 140)
keyPanel.Position = UDim2.new(0.5, -170, 0.5, -70)
keyPanel.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
keyPanel.BorderSizePixel = 0
keyPanel.Parent = gui
Instance.new("UICorner", keyPanel).CornerRadius = UDim.new(0.26,0)
local keyStroke = Instance.new("UIStroke", keyPanel)
keyStroke.Color = Color3.fromRGB(90,90,90)
keyStroke.Thickness = 2

local keyTitle = Instance.new("TextLabel", keyPanel)
keyTitle.Size = UDim2.new(1,0,0,36)
keyTitle.Position = UDim2.new(0,0,0,9)
keyTitle.BackgroundTransparency = 1
keyTitle.Text = "PAINEL XLZIN"
keyTitle.Font = Enum.Font.GothamBold
keyTitle.TextColor3 = Color3.fromRGB(180,180,180)
keyTitle.TextScaled = true

local keyLabel = Instance.new("TextLabel", keyPanel)
keyLabel.Size = UDim2.new(1,0,0,22)
keyLabel.Position = UDim2.new(0,0,0,43)
keyLabel.BackgroundTransparency = 1
keyLabel.Text = "Digite a KEY para acessar:"
keyLabel.Font = Enum.Font.Gotham
keyLabel.TextColor3 = Color3.fromRGB(210,210,210)
keyLabel.TextScaled = true

local keyInput = Instance.new("TextBox", keyPanel)
keyInput.Size = UDim2.new(0.77,0,0,28)
keyInput.Position = UDim2.new(0.115,0,0,69)
keyInput.PlaceholderText = "KEY aqui"
keyInput.Font = Enum.Font.Gotham
keyInput.Text = ""
keyInput.TextColor3 = Color3.fromRGB(255,255,255)
keyInput.BackgroundColor3 = Color3.fromRGB(40,40,40)
keyInput.TextScaled = true
Instance.new("UICorner", keyInput).CornerRadius = UDim.new(0.33,0)

local keyBtn = Instance.new("TextButton", keyPanel)
keyBtn.Size = UDim2.new(0.45,0,0,22)
keyBtn.Position = UDim2.new(0.275,0,0,105)
keyBtn.Text = "ENTRAR"
keyBtn.Font = Enum.Font.GothamBold
keyBtn.TextColor3 = Color3.fromRGB(255,255,255)
keyBtn.BackgroundColor3 = Color3.fromRGB(60,60,60)
keyBtn.TextScaled = true
Instance.new("UICorner", keyBtn).CornerRadius = UDim.new(0.5,0)

local keyStatus = Instance.new("TextLabel", keyPanel)
keyStatus.Size = UDim2.new(1,0,0,15)
keyStatus.Position = UDim2.new(0,0,0,124)
keyStatus.BackgroundTransparency = 1
keyStatus.Text = ""
keyStatus.TextScaled = true
keyStatus.Font = Enum.Font.Gotham
keyStatus.TextColor3 = Color3.fromRGB(255,80,80)

-- Painel principal preto (arredondado, borda cinza, minimizar/restaurar)
local painel = Instance.new("Frame", gui)
painel.Size = UDim2.new(0, 420, 0, 330)
painel.Position = UDim2.new(0.5, -210, 0.5, -165)
painel.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
painel.Visible = false
painel.BorderSizePixel = 0
Instance.new("UICorner", painel).CornerRadius = UDim.new(0.23,0)
local painelStroke = Instance.new("UIStroke", painel)
painelStroke.Color = Color3.fromRGB(90,90,90)
painelStroke.Thickness = 2

local painelTitle = Instance.new("TextLabel", painel)
painelTitle.Size = UDim2.new(1,0,0,38)
painelTitle.Position = UDim2.new(0,0,0,0)
painelTitle.BackgroundTransparency = 1
painelTitle.Text = "PAINEL LIBERADO"
painelTitle.Font = Enum.Font.GothamBold
painelTitle.TextColor3 = Color3.fromRGB(180,180,180)
painelTitle.TextScaled = true

local bolaMini = Instance.new("TextButton", painel)
bolaMini.Size = UDim2.new(0,28,0,28)
bolaMini.Position = UDim2.new(1, -36, 0, 10)
bolaMini.BackgroundColor3 = Color3.fromRGB(60,60,60)
bolaMini.Text = "-"
bolaMini.TextColor3 = Color3.fromRGB(255,255,255)
bolaMini.Font = Enum.Font.GothamBold
bolaMini.TextScaled = true
Instance.new("UICorner", bolaMini).CornerRadius = UDim.new(1,0)
bolaMini.AutoButtonColor = true

local bolaDesMini = Instance.new("TextButton", gui)
bolaDesMini.Size = UDim2.new(0,28,0,28)
bolaDesMini.Position = UDim2.new(0, 20, 0.65, 0)
bolaDesMini.BackgroundColor3 = Color3.fromRGB(60,60,60)
bolaDesMini.Text = "+"
bolaDesMini.TextColor3 = Color3.fromRGB(255,255,255)
bolaDesMini.Font = Enum.Font.GothamBold
bolaDesMini.TextScaled = true
Instance.new("UICorner", bolaDesMini).CornerRadius = UDim.new(1,0)
bolaDesMini.Visible = false
bolaDesMini.AutoButtonColor = true

bolaMini.MouseButton1Click:Connect(function()
    painel.Visible = false
    bolaDesMini.Visible = true
end)
bolaDesMini.MouseButton1Click:Connect(function()
    painel.Visible = true
    bolaDesMini.Visible = false
end)

-- Painel de opções rolável
local optionFrame = Instance.new("Frame")
optionFrame.Name = "OptionFrame"
optionFrame.BackgroundTransparency = 1
optionFrame.Size = UDim2.new(1,0,0.89,0)
optionFrame.Position = UDim2.new(0,0,0.11,0)
optionFrame.Parent = painel

local scroll = Instance.new("ScrollingFrame", optionFrame)
scroll.Size = UDim2.new(1, 0, 1, 0)
scroll.CanvasSize = UDim2.new(0, 0, 1.45, 0)
scroll.BackgroundTransparency = 1
scroll.BorderSizePixel = 0
scroll.ScrollBarThickness = 8
local UIList = Instance.new("UIListLayout", scroll)
UIList.Padding = UDim.new(0.04,0)
UIList.HorizontalAlignment = Enum.HorizontalAlignment.Center
UIList.VerticalAlignment = Enum.VerticalAlignment.Top
UIList.SortOrder = Enum.SortOrder.LayoutOrder

local estado = {esp=false, noclip=false, grudarMira=false, fly=false, invis=false}
local noclipConn, espConns, grudarMiraConn, flyConn = nil, {}, nil, nil
local flyVertical = 0
local UpBtn, DownBtn

local function addToggle(label, stateKey, color)
    local line = Instance.new("Frame")
    line.Size = UDim2.new(0.93,0,0.11,0)
    line.BackgroundTransparency = 1
    line.Parent = scroll

    local check = Instance.new("TextButton")
    check.Size = UDim2.new(0,32,1,0)
    check.Position = UDim2.new(0,0,0,0)
    check.BackgroundColor3 = color or Color3.fromRGB(60, 60, 60)
    check.Text = " "
    check.Font = Enum.Font.GothamBold
    check.TextColor3 = Color3.fromRGB(255,255,255)
    check.TextScaled = true
    check.Parent = line
    Instance.new("UICorner", check).CornerRadius = UDim.new(1,0)

    local txt = Instance.new("TextLabel")
    txt.Size = UDim2.new(1, -40, 1, 0)
    txt.Position = UDim2.new(0,40,0,0)
    txt.BackgroundTransparency = 1
    txt.Text = label
    txt.Font = Enum.Font.GothamBold
    txt.TextColor3 = Color3.fromRGB(200,200,200)
    txt.TextScaled = true
    txt.Parent = line

    local function update()
        if estado[stateKey] then
            check.Text = "✔"
            check.BackgroundColor3 = Color3.fromRGB(130, 130, 130)
        else
            check.Text = " "
            check.BackgroundColor3 = color or Color3.fromRGB(60, 60, 60)
        end
    end

    check.MouseButton1Click:Connect(function()
        estado[stateKey] = not estado[stateKey]
        update()
        if stateKey == "esp" then
            if estado.esp then ativarESP() else desativarESP() end
        elseif stateKey == "noclip" then
            if estado.noclip then
                if noclipConn then noclipConn:Disconnect() end
                noclipConn = game:GetService("RunService").Stepped:Connect(function()
                    local char = player.Character
                    if char then
                        for _,part in pairs(char:GetChildren()) do
                            if part:IsA("BasePart") then
                                part.CanCollide = false
                            end
                        end
                    end
                end)
            else
                if noclipConn then noclipConn:Disconnect() end
                local char = player.Character
                if char then
                    for _,part in pairs(char:GetChildren()) do
                        if part:IsA("BasePart") then
                            if part.Name == "HumanoidRootPart" or part.Name == "Torso" or part.Name == "UpperTorso" or part.Name == "LowerTorso" or part.Name == "Head" then
                                part.CanCollide = true
                            end
                        end
                    end
                end
            end
        elseif stateKey == "grudarMira" then
            if estado.grudarMira then
                startGrudarMira()
            else
                stopGrudarMira()
            end
        elseif stateKey == "fly" then
            if estado.fly then ativarFly() else desativarFly() end
        elseif stateKey == "invis" then
            if estado.invis then ativarInvisibilidade() else desativarInvisibilidade() end
        end
    end)
    update()
    return line
end

addToggle("ESP", "esp", Color3.fromRGB(60, 60, 60))
addToggle("ATRAVESSAR PAREDE", "noclip", Color3.fromRGB(60, 60, 60))
addToggle("GRUDAR MIRA", "grudarMira", Color3.fromRGB(120, 60, 120))
addToggle("FLY (mobile/setas)", "fly", Color3.fromRGB(60, 80, 100))
addToggle("INVISIBILIDADE", "invis", Color3.fromRGB(60, 100, 60))

local speedBtn = Instance.new("TextButton")
speedBtn.Size = UDim2.new(0.93,0,0.11,0)
speedBtn.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
speedBtn.Text = "VELOCIDADE"
speedBtn.TextColor3 = Color3.fromRGB(210,210,210)
speedBtn.TextScaled = true
speedBtn.Font = Enum.Font.GothamBold
speedBtn.Parent = scroll
Instance.new("UICorner", speedBtn).CornerRadius = UDim.new(0.22,0)

local speedGui = Instance.new("Frame")
speedGui.Name = "SpeedSelectorFrame"
speedGui.Size = UDim2.new(0, 300, 0, 200)
speedGui.Position = UDim2.new(0.5, -150, 0.16, 0)
speedGui.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
speedGui.BackgroundTransparency = 0.09
speedGui.BorderSizePixel = 0
speedGui.AnchorPoint = Vector2.new(0, 0)
speedGui.Parent = gui
speedGui.Visible = false
Instance.new("UICorner", speedGui).CornerRadius = UDim.new(0, 16)

local speedTitle = Instance.new("TextLabel")
speedTitle.Size = UDim2.new(1, 0, 0, 48)
speedTitle.BackgroundTransparency = 1
speedTitle.Text = "Velocidade do Jogador"
speedTitle.Font = Enum.Font.GothamBold
speedTitle.TextSize = 21
speedTitle.TextColor3 = Color3.fromRGB(180, 180, 180)
speedTitle.Parent = speedGui

local speedMinButton = Instance.new("TextButton")
speedMinButton.Size = UDim2.new(0, 36, 0, 36)
speedMinButton.Position = UDim2.new(1, -42, 0, 8)
speedMinButton.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
speedMinButton.Text = "_"
speedMinButton.Font = Enum.Font.GothamBold
speedMinButton.TextSize = 28
speedMinButton.TextColor3 = Color3.fromRGB(180, 180, 180)
speedMinButton.Parent = speedGui
Instance.new("UICorner", speedMinButton).CornerRadius = UDim.new(1, 0)

local speedRestoreButton = Instance.new("TextButton")
speedRestoreButton.Size = UDim2.new(0, 50, 0, 36)
speedRestoreButton.Position = UDim2.new(0, 10, 1, -46)
speedRestoreButton.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
speedRestoreButton.Text = "Abrir"
speedRestoreButton.Font = Enum.Font.GothamBold
speedRestoreButton.TextSize = 18
speedRestoreButton.TextColor3 = Color3.fromRGB(200, 200, 200)
speedRestoreButton.Visible = false
speedRestoreButton.Parent = gui
Instance.new("UICorner", speedRestoreButton).CornerRadius = UDim.new(1, 0)

local options = {
    {Name = "Baixa (lenta)", Speed = 8, Color = Color3.fromRGB(90, 90, 90)},
    {Name = "Média", Speed = 16, Color = Color3.fromRGB(70, 120, 150)},
    {Name = "Rápida", Speed = 150, Color = Color3.fromRGB(120, 60, 120)},
}
for i, opt in ipairs(options) do
    local button = Instance.new("TextButton")
    button.Size = UDim2.new(0.8, 0, 0, 36)
    button.Position = UDim2.new(0.1, 0, 0, 50 + (i-1)*46)
    button.BackgroundColor3 = opt.Color
    button.Text = opt.Name
    button.Font = Enum.Font.Gotham
    button.TextSize = 20
    button.TextColor3 = Color3.fromRGB(255,255,255)
    button.AutoButtonColor = true
    button.Parent = speedGui
    Instance.new("UICorner", button).CornerRadius = UDim.new(0, 12)
    button.MouseButton1Click:Connect(function()
        local char = player.Character or player.CharacterAdded:Wait()
        local humanoid = char:FindFirstChildOfClass("Humanoid")
        if humanoid then
            humanoid.WalkSpeed = opt.Speed
        end
    end)
end
speedMinButton.MouseButton1Click:Connect(function()
    speedGui.Visible = false
    speedRestoreButton.Visible = true
end)
speedRestoreButton.MouseButton1Click:Connect(function()
    speedGui.Visible = true
    speedRestoreButton.Visible = false
end)
speedBtn.MouseButton1Click:Connect(function()
    speedGui.Visible = not speedGui.Visible
    speedRestoreButton.Visible = false
end)

-- Funções ESP
espConns = {}

-- HIGHLIGHT TODOS INIMIGOS (INDEPENDENTE DA DISTÂNCIA)
local allEnemyHighlights = {}
local function isEnemy(p)
    if p.Team ~= nil and player.Team ~= nil then
        return p.Team ~= player.Team
    end
    return true -- Se não houver Team, considera todos inimigos
end

local function highlightAllEnemies()
    -- Remove highlights antigos
    for _, h in pairs(allEnemyHighlights) do
        pcall(function() h:Destroy() end)
    end
    allEnemyHighlights = {}

    for _,p in pairs(game.Players:GetPlayers()) do
        if p ~= player and isEnemy(p) and p.Character and p.Character:FindFirstChild("HumanoidRootPart") then
            local exists = false
            for _, h in pairs(game:GetService("CoreGui"):GetChildren()) do
                if h:IsA("Highlight") and h.Name == "EnemyGlobalHighlight" and h.Adornee == p.Character then
                    exists = true
                    table.insert(allEnemyHighlights, h)
                end
            end
            if not exists then
                local highlight = Instance.new("Highlight")
                highlight.Name = "EnemyGlobalHighlight"
                highlight.FillColor = Color3.fromRGB(255,0,0)
                highlight.OutlineColor = Color3.fromRGB(255,0,0)
                highlight.FillTransparency = 0.7
                highlight.OutlineTransparency = 0
                highlight.Adornee = p.Character
                highlight.Parent = game:GetService("CoreGui")
                table.insert(allEnemyHighlights, highlight)
            end
        end
    end
end

local function removeAllEnemyHighlights()
    for _, h in pairs(allEnemyHighlights) do
        pcall(function() h:Destroy() end)
    end
    allEnemyHighlights = {}
    for _, h in pairs(game:GetService("CoreGui"):GetChildren()) do
        if h:IsA("Highlight") and h.Name == "EnemyGlobalHighlight" then
            pcall(function() h:Destroy() end)
        end
    end
end

function ativarESP()
    for _,conn in pairs(espConns) do pcall(function() conn:Disconnect() end) end
    espConns = {}
    local function createEspForPlayer(target)
        if target == player then return end
        local billboard = Instance.new("BillboardGui")
        billboard.Name = "ESP_XL"
        billboard.AlwaysOnTop = true
        billboard.Size = UDim2.new(0,120,0,32)
        billboard.StudsOffset = Vector3.new(0,3,0)
        billboard.Adornee = (target.Character and target.Character:FindFirstChild("Head")) or nil
        billboard.Parent = game:GetService("CoreGui")
        local label = Instance.new("TextLabel", billboard)
        label.Size = UDim2.new(1,0,1,0)
        label.BackgroundTransparency = 1
        label.TextColor3 = Color3.new(1,1,1)
        label.TextStrokeTransparency = 0.4
        label.TextScaled = true
        label.Font = Enum.Font.GothamBold
        label.Text = ""
        local updateConn
        updateConn = game:GetService("RunService").RenderStepped:Connect(function()
            if not estado.esp or not target.Parent then
                billboard:Destroy()
                if updateConn then updateConn:Disconnect() end
                return
            end
            if not target.Character or not target.Character:FindFirstChild("Head") then
                billboard.Adornee = nil
                label.Text = ""
            else
                billboard.Adornee = target.Character.Head
                local dist = math.floor((player.Character and player:DistanceFromCharacter(target.Character.Head.Position)) or 0)
                label.Text = target.Name .. " [" .. dist .. "m]"
            end
        end)
        table.insert(espConns, updateConn)
    end
    for _,p in pairs(game.Players:GetPlayers()) do
        if p ~= player then createEspForPlayer(p) end
    end
    local plrConn = game.Players.PlayerAdded:Connect(function(p)
        createEspForPlayer(p)
    end)
    table.insert(espConns, plrConn)
    highlightAllEnemies()
end
function desativarESP()
    for _,conn in pairs(espConns) do pcall(function() conn:Disconnect() end) end
    espConns = {}
    for _,guiObj in pairs(game:GetService("CoreGui"):GetChildren()) do
        if guiObj.Name == "ESP_XL" then guiObj:Destroy() end
    end
    removeAllEnemyHighlights()
end

-- GRUDAR MIRA SÓ EM INIMIGOS/OUTRO TIME, mas highlight vermelho em todos
local GRUDAR_MIRA_RANGE = 80
local aimlockHighlight
local grudarMiraConn
local hitboxParts = {}

local function getClosestEnemyPlayerRange()
    local closest, dist = nil, math.huge
    for _, p in pairs(game.Players:GetPlayers()) do
        if p ~= player and isEnemy(p) and p.Character and p.Character:FindFirstChild("Head") and p.Character:FindFirstChild("Humanoid") and p.Character.Humanoid.Health > 0 then
            local char = player.Character
            if char and char:FindFirstChild("Head") then
                local d = (char.Head.Position - p.Character.Head.Position).Magnitude
                if d < dist and d < GRUDAR_MIRA_RANGE then
                    dist = d
                    closest = p
                end
            end
        end
    end
    return closest
end

local function setHitboxSize(target, big)
    if not target or not target.Character then return end
    for _, part in pairs(target.Character:GetChildren()) do
        if part:IsA("BasePart") and part.Name ~= "HumanoidRootPart" then
            if big then
                if not hitboxParts[part] then
                    hitboxParts[part] = part.Size
                    part.Size = part.Size * 2
                    part.Transparency = 0.4
                    part.Color = Color3.new(1,0,0)
                end
            else
                if hitboxParts[part] then
                    part.Size = hitboxParts[part]
                    part.Transparency = 0
                    part.Color = part.Color
                    hitboxParts[part] = nil
                end
            end
        end
    end
end

local function updateAimlockHighlight(target)
    if aimlockHighlight then
        pcall(function() aimlockHighlight:Destroy() end)
        aimlockHighlight = nil
    end
    if target and target.Character and target.Character:FindFirstChild("HumanoidRootPart") then
        local highlight = Instance.new("Highlight")
        highlight.Name = "GrudarMiraHighlight"
        highlight.FillColor = Color3.fromRGB(255,0,0)
        highlight.OutlineColor = Color3.fromRGB(255,0,0)
        highlight.FillTransparency = 0.7
        highlight.OutlineTransparency = 0
        highlight.Adornee = target.Character
        highlight.Parent = game:GetService("CoreGui")
        aimlockHighlight = highlight
    end
end

function startGrudarMira()
    if grudarMiraConn then grudarMiraConn:Disconnect() end
    highlightAllEnemies()
    grudarMiraConn = game:GetService("RunService").RenderStepped:Connect(function()
        if not estado.grudarMira then
            updateAimlockHighlight(nil)
            removeAllEnemyHighlights()
            for _, p in pairs(game.Players:GetPlayers()) do
                if p ~= player then setHitboxSize(p,false) end
            end
            return
        end

        highlightAllEnemies()

        local target = getClosestEnemyPlayerRange()
        if target and target.Character and target.Character:FindFirstChild("Head") then
            local cam = workspace.CurrentCamera
            cam.CFrame = CFrame.new(cam.CFrame.Position, target.Character.Head.Position)
            setHitboxSize(target,true)
            for _, p in pairs(game.Players:GetPlayers()) do
                if p ~= player and p ~= target then setHitboxSize(p,false) end
            end
            updateAimlockHighlight(target)
        else
            updateAimlockHighlight(nil)
            for _, p in pairs(game.Players:GetPlayers()) do
                if p ~= player then setHitboxSize(p,false) end
            end
        end
    end)
end

function stopGrudarMira()
    if grudarMiraConn then grudarMiraConn:Disconnect() end
    updateAimlockHighlight(nil)
    removeAllEnemyHighlights()
    for _, p in pairs(game.Players:GetPlayers()) do
        if p ~= player then setHitboxSize(p,false) end
    end
end

-- FLY (mobile/setas)
function ativarFly()
    if flyConn then flyConn:Disconnect() end
    local char = player.Character or player.CharacterAdded:Wait()
    local humanoid = char:FindFirstChildOfClass("Humanoid")
    local hrp = char:FindFirstChild("HumanoidRootPart")
    if not humanoid or not hrp then return end
    humanoid.PlatformStand = true

    if not UpBtn then
        UpBtn = Instance.new("TextButton")
        UpBtn.Size = UDim2.new(0, 44, 0, 44)
        UpBtn.Position = UDim2.new(1, -110, 1, -180)
        UpBtn.AnchorPoint = Vector2.new(0.5,0.5)
        UpBtn.BackgroundColor3 = Color3.fromRGB(140, 60, 230)
        UpBtn.Text = "▲"
        UpBtn.TextScaled = true
        UpBtn.Font = Enum.Font.GothamBold
        UpBtn.TextColor3 = Color3.new(1,1,1)
        Instance.new("UICorner", UpBtn).CornerRadius = UDim.new(1,0)
        UpBtn.Parent = gui
        UpBtn.Visible = false
        UpBtn.MouseButton1Down:Connect(function() flyVertical = 1 end)
        UpBtn.MouseButton1Up:Connect(function() flyVertical = 0 end)
        UpBtn.TouchTap:Connect(function() flyVertical = 1 end)
        UpBtn.TouchLongPress:Connect(function() flyVertical = 0 end)
    end
    if not DownBtn then
        DownBtn = Instance.new("TextButton")
        DownBtn.Size = UDim2.new(0, 44, 0, 44)
        DownBtn.Position = UDim2.new(1, -110, 1, -120)
        DownBtn.AnchorPoint = Vector2.new(0.5,0.5)
        DownBtn.BackgroundColor3 = Color3.fromRGB(70, 140, 255)
        DownBtn.Text = "▼"
        DownBtn.TextScaled = true
        DownBtn.Font = Enum.Font.GothamBold
        DownBtn.TextColor3 = Color3.new(1,1,1)
        Instance.new("UICorner", DownBtn).CornerRadius = UDim.new(1,0)
        DownBtn.Parent = gui
        DownBtn.Visible = false
        DownBtn.MouseButton1Down:Connect(function() flyVertical = -1 end)
        DownBtn.MouseButton1Up:Connect(function() flyVertical = 0 end)
        DownBtn.TouchTap:Connect(function() flyVertical = -1 end)
        DownBtn.TouchLongPress:Connect(function() flyVertical = 0 end)
    end
    UpBtn.Visible = true
    DownBtn.Visible = true

    flyConn = game:GetService("RunService").RenderStepped:Connect(function()
        if not estado.fly then return end
        if not humanoid or not humanoid.Parent then return end
        local moveDir = humanoid.MoveDirection
        local vertical = flyVertical * 50
        hrp.Velocity = Vector3.new(moveDir.X * 50, vertical, moveDir.Z * 50)
    end)
end

function desativarFly()
    if flyConn then flyConn:Disconnect() end
    local char = player.Character
    if char and char:FindFirstChildOfClass("Humanoid") then
        char:FindFirstChildOfClass("Humanoid").PlatformStand = false
    end
    local hrp = char and char:FindFirstChild("HumanoidRootPart")
    if hrp then hrp.Velocity = Vector3.new(0,0,0) end
    if UpBtn then UpBtn.Visible = false end
    if DownBtn then DownBtn.Visible = false end
    flyVertical = 0
end

-- INVISIBILIDADE
local invisParts = {}
function ativarInvisibilidade()
    local char = player.Character or player.CharacterAdded:Wait()
    for _,v in pairs(char:GetChildren()) do
        if v:IsA("BasePart") and v.Name ~= "HumanoidRootPart" then
            invisParts[v] = v.Transparency
            v.Transparency = 1
            if v:FindFirstChildOfClass("Decal") then
                for _,d in pairs(v:GetChildren()) do
                    if d:IsA("Decal") then
                        d.Transparency = 1
                    end
                end
            end
            if v:FindFirstChildOfClass("Texture") then
                for _,d in pairs(v:GetChildren()) do
                    if d:IsA("Texture") then
                        d.Transparency = 1
                    end
                end
            end
        end
    end
end
function desativarInvisibilidade()
    local char = player.Character or player.CharacterAdded:Wait()
    for _,v in pairs(char:GetChildren()) do
        if v:IsA("BasePart") and invisParts[v] then
            v.Transparency = invisParts[v]
            if v:FindFirstChildOfClass("Decal") then
                for _,d in pairs(v:GetChildren()) do
                    if d:IsA("Decal") then
                        d.Transparency = 0
                    end
                end
            end
            if v:FindFirstChildOfClass("Texture") then
                for _,d in pairs(v:GetChildren()) do
                    if d:IsA("Texture") then
                        d.Transparency = 0
                    end
                end
            end
        end
    end
    invisParts = {}
end

-- MANTER FUNÇÕES ATIVAS APÓS MORRER/RESPAWN
player.CharacterAdded:Connect(function()
    wait(1)
    if estado.esp then ativarESP() end
    if estado.noclip then
        if noclipConn then noclipConn:Disconnect() end
        noclipConn = game:GetService("RunService").Stepped:Connect(function()
            local char = player.Character
            if char then
                for _,part in pairs(char:GetChildren()) do
                    if part:IsA("BasePart") then
                        part.CanCollide = false
                    end
                end
            end
        end)
    end
    if estado.grudarMira then startGrudarMira() end
    if estado.fly then ativarFly() end
    if estado.invis then ativarInvisibilidade() end
    if estado.esp or estado.grudarMira then
        highlightAllEnemies()
    end
end)

game.Players.PlayerAdded:Connect(function()
    if estado.esp or estado.grudarMira then
        highlightAllEnemies()
    end
end)
game.Players.PlayerRemoving:Connect(function()
    if estado.esp or estado.grudarMira then
        highlightAllEnemies()
    end
end)

-- ENVIAR KEY
keyBtn.MouseButton1Click:Connect(function()
    if keyInput.Text == KEY_CORRETA then
        keyStatus.Text = ""
        keyPanel.Visible = false
        painel.Visible = true
    else
        keyStatus.Text = "Key inválida!"
        keyStatus.TextColor3 = Color3.fromRGB(255,80,80)
    end
end)
