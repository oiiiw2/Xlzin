-- Painel Roxo Moderno: KEY, VELOCIDADE, ESP, ATRAVESSAR PAREDE, GRUDAR MIRA, FLY (SETAS), INVISIBILIDADE, VIDA INFINITA
-- Feito por XLZIN (versão ajustada e expandida)

local KEY_CORRETA = "sxTKQP365"
local player = game.Players.LocalPlayer

-- GUI principal
local gui = Instance.new("ScreenGui")
gui.Name = "PainelXLZIN"
gui.Parent = game:GetService("CoreGui")
gui.ResetOnSpawn = false

-- Painel de Key (roxo, arredondado)
local keyPanel = Instance.new("Frame")
keyPanel.Name = "KeyPanel"
keyPanel.Size = UDim2.new(0, 340, 0, 140)
keyPanel.Position = UDim2.new(0.5, -170, 0.5, -70)
keyPanel.BackgroundColor3 = Color3.fromRGB(40, 18, 60)
keyPanel.BorderSizePixel = 0
keyPanel.Parent = gui
Instance.new("UICorner", keyPanel).CornerRadius = UDim.new(0.26,0)
local keyStroke = Instance.new("UIStroke", keyPanel)
keyStroke.Color = Color3.fromRGB(160,60,220)
keyStroke.Thickness = 2

local keyTitle = Instance.new("TextLabel", keyPanel)
keyTitle.Size = UDim2.new(1,0,0,36)
keyTitle.Position = UDim2.new(0,0,0,9)
keyTitle.BackgroundTransparency = 1
keyTitle.Text = "PAINEL XLZIN"
keyTitle.Font = Enum.Font.GothamBold
keyTitle.TextColor3 = Color3.fromRGB(210,160,255)
keyTitle.TextScaled = true

local keyLabel = Instance.new("TextLabel", keyPanel)
keyLabel.Size = UDim2.new(1,0,0,22)
keyLabel.Position = UDim2.new(0,0,0,43)
keyLabel.BackgroundTransparency = 1
keyLabel.Text = "Digite a KEY para acessar:"
keyLabel.Font = Enum.Font.Gotham
keyLabel.TextColor3 = Color3.fromRGB(230,230,250)
keyLabel.TextScaled = true

local keyInput = Instance.new("TextBox", keyPanel)
keyInput.Size = UDim2.new(0.77,0,0,28)
keyInput.Position = UDim2.new(0.115,0,0,69)
keyInput.PlaceholderText = "KEY aqui"
keyInput.Font = Enum.Font.Gotham
keyInput.Text = ""
keyInput.TextColor3 = Color3.fromRGB(255,255,255)
keyInput.BackgroundColor3 = Color3.fromRGB(60, 30, 110)
keyInput.TextScaled = true
Instance.new("UICorner", keyInput).CornerRadius = UDim.new(0.33,0)

local keyBtn = Instance.new("TextButton", keyPanel)
keyBtn.Size = UDim2.new(0.45,0,0,22)
keyBtn.Position = UDim2.new(0.275,0,0,105)
keyBtn.Text = "ENTRAR"
keyBtn.Font = Enum.Font.GothamBold
keyBtn.TextColor3 = Color3.fromRGB(255,255,255)
keyBtn.BackgroundColor3 = Color3.fromRGB(130,60,210)
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

-- Painel principal roxo (arredondado, borda roxa, minimizar/restaurar)
local painel = Instance.new("Frame", gui)
painel.Size = UDim2.new(0, 420, 0, 295)
painel.Position = UDim2.new(0.5, -210, 0.5, -147)
painel.BackgroundColor3 = Color3.fromRGB(38, 10, 60)
painel.Visible = false
painel.BorderSizePixel = 0
Instance.new("UICorner", painel).CornerRadius = UDim.new(0.23,0)
local painelStroke = Instance.new("UIStroke", painel)
painelStroke.Color = Color3.fromRGB(160,60,220)
painelStroke.Thickness = 2

local painelTitle = Instance.new("TextLabel", painel)
painelTitle.Size = UDim2.new(1,0,0,38)
painelTitle.Position = UDim2.new(0,0,0,0)
painelTitle.BackgroundTransparency = 1
painelTitle.Text = "PAINEL LIBERADO"
painelTitle.Font = Enum.Font.GothamBold
painelTitle.TextColor3 = Color3.fromRGB(210,160,255)
painelTitle.TextScaled = true

local bolaMini = Instance.new("TextButton", painel)
bolaMini.Size = UDim2.new(0,28,0,28)
bolaMini.Position = UDim2.new(1, -36, 0, 10)
bolaMini.BackgroundColor3 = Color3.fromRGB(160,60,220)
bolaMini.Text = "-"
bolaMini.TextColor3 = Color3.fromRGB(255,255,255)
bolaMini.Font = Enum.Font.GothamBold
bolaMini.TextScaled = true
Instance.new("UICorner", bolaMini).CornerRadius = UDim.new(1,0)
bolaMini.AutoButtonColor = true

local bolaDesMini = Instance.new("TextButton", gui)
bolaDesMini.Size = UDim2.new(0,28,0,28)
bolaDesMini.Position = UDim2.new(0, 20, 0.65, 0)
bolaDesMini.BackgroundColor3 = Color3.fromRGB(160,60,220)
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

-- Funções principais do painel (Checks modernos)
local optionFrame = Instance.new("Frame")
optionFrame.Name = "OptionFrame"
optionFrame.BackgroundTransparency = 1
optionFrame.Size = UDim2.new(1,0,0.89,0)
optionFrame.Position = UDim2.new(0,0,0.11,0)
optionFrame.Parent = painel

local UIList = Instance.new("UIListLayout", optionFrame)
UIList.Padding = UDim.new(0.04,0)
UIList.HorizontalAlignment = Enum.HorizontalAlignment.Center
UIList.VerticalAlignment = Enum.VerticalAlignment.Top
UIList.SortOrder = Enum.SortOrder.LayoutOrder

local estado = {esp=false, noclip=false, grudarMira=false, fly=false, invis=false, god=false}
local noclipConn, espConns, miraConn, flyConn, godConn = nil, {}, nil, nil, nil
local flyVertical = 0
local UpBtn, DownBtn = nil, nil

local function addToggle(label, stateKey, color)
    local line = Instance.new("Frame")
    line.Size = UDim2.new(0.93,0,0.11,0)
    line.BackgroundTransparency = 1
    line.Parent = optionFrame

    local check = Instance.new("TextButton")
    check.Size = UDim2.new(0,32,1,0)
    check.Position = UDim2.new(0,0,0,0)
    check.BackgroundColor3 = color or Color3.fromRGB(90, 70, 140)
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
    txt.TextColor3 = Color3.fromRGB(220,220,230)
    txt.TextScaled = true
    txt.Parent = line

    local function update()
        if estado[stateKey] then
            check.Text = "✔"
            check.BackgroundColor3 = Color3.fromRGB(140, 60, 230)
        else
            check.Text = " "
            check.BackgroundColor3 = color or Color3.fromRGB(90, 70, 140)
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
        elseif stateKey == "god" then
            if estado.god then ativarGodMode() else desativarGodMode() end
        end
    end)
    update()
    return line
end

addToggle("ESP", "esp", Color3.fromRGB(140, 60, 230))
addToggle("ATRAVESSAR PAREDE", "noclip", Color3.fromRGB(120, 80, 230))
addToggle("GRUDAR MIRA", "grudarMira", Color3.fromRGB(90, 160, 255))
addToggle("FLY (analógico)", "fly", Color3.fromRGB(120, 180, 230))
addToggle("INVISIBILIDADE", "invis", Color3.fromRGB(70,200,150))
addToggle("VIDA INFINITA", "god", Color3.fromRGB(255, 80, 130))

-- Painel de velocidade roxo
local speedBtn = Instance.new("TextButton")
speedBtn.Size = UDim2.new(0.93,0,0.11,0)
speedBtn.BackgroundColor3 = Color3.fromRGB(90, 50, 140)
speedBtn.Text = "VELOCIDADE"
speedBtn.TextColor3 = Color3.fromRGB(220,220,250)
speedBtn.TextScaled = true
speedBtn.Font = Enum.Font.GothamBold
speedBtn.Parent = optionFrame
Instance.new("UICorner", speedBtn).CornerRadius = UDim.new(0.22,0)

local speedGui = Instance.new("Frame")
speedGui.Name = "SpeedSelectorFrame"
speedGui.Size = UDim2.new(0, 300, 0, 200)
speedGui.Position = UDim2.new(0.5, -150, 0.16, 0)
speedGui.BackgroundColor3 = Color3.fromRGB(60, 20, 100)
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
speedTitle.TextColor3 = Color3.fromRGB(240, 220, 255)
speedTitle.Parent = speedGui

local speedMinButton = Instance.new("TextButton")
speedMinButton.Size = UDim2.new(0, 36, 0, 36)
speedMinButton.Position = UDim2.new(1, -42, 0, 8)
speedMinButton.BackgroundColor3 = Color3.fromRGB(120, 80, 180)
speedMinButton.Text = "_"
speedMinButton.Font = Enum.Font.GothamBold
speedMinButton.TextSize = 28
speedMinButton.TextColor3 = Color3.fromRGB(200, 200, 255)
speedMinButton.Parent = speedGui
Instance.new("UICorner", speedMinButton).CornerRadius = UDim.new(1, 0)

local speedRestoreButton = Instance.new("TextButton")
speedRestoreButton.Size = UDim2.new(0, 50, 0, 36)
speedRestoreButton.Position = UDim2.new(0, 10, 1, -46)
speedRestoreButton.BackgroundColor3 = Color3.fromRGB(120, 80, 180)
speedRestoreButton.Text = "Abrir"
speedRestoreButton.Font = Enum.Font.GothamBold
speedRestoreButton.TextSize = 18
speedRestoreButton.TextColor3 = Color3.fromRGB(200, 200, 255)
speedRestoreButton.Visible = false
speedRestoreButton.Parent = gui
Instance.new("UICorner", speedRestoreButton).CornerRadius = UDim.new(1, 0)

local options = {
    {Name = "Baixa (lenta)", Speed = 8, Color = Color3.fromRGB(160, 110, 255)},
    {Name = "Média", Speed = 16, Color = Color3.fromRGB(120, 200, 255)},
    {Name = "Rápida", Speed = 150, Color = Color3.fromRGB(255, 128, 255)},
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

-- Funções lógicas
espConns = {}
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
end
function desativarESP()
    for _,conn in pairs(espConns) do pcall(function() conn:Disconnect() end) end
    espConns = {}
    for _,guiObj in pairs(game:GetService("CoreGui"):GetChildren()) do
        if guiObj.Name == "ESP_XL" then guiObj:Destroy() end
    end
end

-- Grudar Mira
local function getClosestPlayer()
    local closest, dist = nil, math.huge
    for _, p in pairs(game.Players:GetPlayers()) do
        if p ~= player and p.Character and p.Character:FindFirstChild("Head") then
            local char = player.Character
            if char and char:FindFirstChild("Head") then
                local d = (char.Head.Position - p.Character.Head.Position).Magnitude
                if d < dist then
                    dist = d
                    closest = p
                end
            end
        end
    end
    return closest
end
local function isArmed()
    local char = player.Character
    if not char then return false end
    for _,v in pairs(char:GetChildren()) do
        if v:IsA("Tool") and (v:FindFirstChild("Handle") or v:FindFirstChildWhichIsA("Part")) then
            return v
        end
    end
    return false
end
function startGrudarMira()
    if miraConn then miraConn:Disconnect() end
    miraConn = game:GetService("RunService").RenderStepped:Connect(function()
        if not estado.grudarMira then return end
        local arma = isArmed()
        if arma then
            local target = getClosestPlayer()
            if target and target.Character and target.Character:FindFirstChild("Head") then
                local cam = workspace.CurrentCamera
                cam.CFrame = CFrame.new(cam.CFrame.Position, target.Character.Head.Position)
            end
        end
    end)
end
function stopGrudarMira()
    if miraConn then miraConn:Disconnect() end
end

-- FLY (com setas)
function ativarFly()
    if flyConn then flyConn:Disconnect() end
    local char = player.Character or player.CharacterAdded:Wait()
    local humanoid = char:FindFirstChildOfClass("Humanoid")
    local hrp = char:FindFirstChild("HumanoidRootPart")
    if not humanoid or not hrp then return end
    humanoid.PlatformStand = true

    -- Setas de fly só aparecem durante o fly
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

-- VIDA INFINITA (GodMode)
function ativarGodMode()
    if godConn then godConn:Disconnect() end
    godConn = game:GetService("RunService").RenderStepped:Connect(function()
        if not estado.god then return end
        local char = player.Character
        if char then
            local hum = char:FindFirstChildOfClass("Humanoid")
            if hum and hum.Health < hum.MaxHealth then
                hum.Health = hum.MaxHealth
            end
        end
    end)
end

function desativarGodMode()
    if godConn then godConn:Disconnect() end
end

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
