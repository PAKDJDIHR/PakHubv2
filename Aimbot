--[[
    ██████╗  █████╗ ██╗  ██╗    ██╗  ██╗██╗   ██╗██████╗ 
    ██╔══██╗██╔══██╗██║ ██╔╝    ██║  ██║██║   ██║██╔══██╗
    ██████╔╝███████║█████╔╝     ███████║██║   ██║██████╔╝
    ██╔═══╝ ██╔══██║██╔═██╗     ██╔══██║██║   ██║██╔══██╗
    ██║     ██║  ██║██║  ██╗    ██║  ██║╚██████╔╝██████╔╝
    ╚═╝     ╚═╝  ╚═╝╚═╝  ╚═╝    ╚═╝  ╚═╝ ╚═════╝ ╚═════╝ 
                    PAK HUB V2 - PARTE 1
]]

--// SERVIÇOS
local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local TweenService = game:GetService("TweenService")
local CoreGui = game:GetService("CoreGui")
local StarterGui = game:GetService("StarterGui")

--// CONFIGURAÇÕES
local CONFIG = {
    KEY_CORRETA = "PakDev2",
    CRIADOR = "PAKDJDIHR",
    COR_PRIMARIA = Color3.fromRGB(138, 43, 226),
    COR_SECUNDARIA = Color3.fromRGB(180, 80, 255),
    COR_FUNDO = Color3.fromRGB(20, 15, 30),
    COR_PAINEL = Color3.fromRGB(30, 22, 45),
    COR_TEXTO = Color3.fromRGB(240, 240, 255),
    COR_SUBTEXTO = Color3.fromRGB(160, 150, 180),
    FONTE = Enum.Font.GothamMedium,
    FONTE_BOLD = Enum.Font.GothamBold,
}

local LocalPlayer = Players.LocalPlayer
local Mouse = LocalPlayer:GetMouse()
local Camera = workspace.CurrentCamera

--// ESTADOS
local State = {
    Aimbot = false,
    AimbotFOV = 120,
    ESP = false,
    Box = false,
    Lines = false,
    Name = false,
    Distance = false,
    Health = false,
    Speed = false,
    SpeedValue = 25,
    Noclip = false,
    Spinbot = false,
    SpinSpeed = 10,
}

--// LIMPAR GUI ANTERIOR
pcall(function()
    if CoreGui:FindFirstChild("PAK_HUB_V2") then
        CoreGui:FindFirstChild("PAK_HUB_V2"):Destroy()
    end
end)
pcall(function()
    if LocalPlayer:FindFirstChild("PlayerGui") and LocalPlayer.PlayerGui:FindFirstChild("PAK_HUB_V2") then
        LocalPlayer.PlayerGui:FindFirstChild("PAK_HUB_V2"):Destroy()
    end
end)

--// CRIAR GUI
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "PAK_HUB_V2"
ScreenGui.ResetOnSpawn = false
ScreenGui.IgnoreGuiInset = true
ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling

local parentGui = (RunService:IsStudio() and LocalPlayer:WaitForChild("PlayerGui")) or CoreGui
ScreenGui.Parent = parentGui

--// FUNÇÕES UTILITÁRIAS
local function criar(className, props)
    local inst = Instance.new(className)
    for k, v in pairs(props) do
        inst[k] = v
    end
    return inst
end

local function arredondar(inst, raio)
    local corner = Instance.new("UICorner")
    corner.CornerRadius = UDim.new(0, raio or 8)
    corner.Parent = inst
end

local function gradiente(inst, c1, c2, rotacao)
    local grad = Instance.new("UIGradient")
    grad.Color = ColorSequence.new(c1, c2)
    grad.Rotation = rotacao or 90
    grad.Parent = inst
end

local function sombra(inst)
    local shadow = Instance.new("UIStroke")
    shadow.Color = CONFIG.COR_PRIMARIA
    shadow.Thickness = 1
    shadow.Transparency = 0.5
    shadow.Parent = inst
end

--// TELA DE KEY
local KeyScreen = criar("Frame", {
    Size = UDim2.new(0, 340, 0, 260),
    Position = UDim2.new(0.5, -170, 0.5, -130),
    BackgroundColor3 = CONFIG.COR_PAINEL,
    BorderSizePixel = 0,
    Parent = ScreenGui,
    ClipsDescendants = true,
})
arredondar(KeyScreen, 14)
gradiente(KeyScreen, CONFIG.COR_PAINEL, CONFIG.COR_FUNDO, 135)
sombra(KeyScreen)

local topBar = criar("Frame", {
    Size = UDim2.new(1, 0, 0, 4),
    BackgroundColor3 = CONFIG.COR_PRIMARIA,
    BorderSizePixel = 0,
    Parent = KeyScreen,
})
gradiente(topBar, CONFIG.COR_PRIMARIA, CONFIG.COR_SECUNDARIA, 0)

local logoLabel = criar("TextLabel", {
    Size = UDim2.new(1, 0, 0, 50),
    Position = UDim2.new(0, 0, 0, 25),
    BackgroundTransparency = 1,
    Text = "PAK HUB V2",
    TextColor3 = CONFIG.COR_TEXTO,
    Font = CONFIG.FONTE_BOLD,
    TextSize = 28,
    Parent = KeyScreen,
})
gradiente(logoLabel, CONFIG.COR_PRIMARIA, CONFIG.COR_SECUNDARIA, 0)

criar("TextLabel", {
    Size = UDim2.new(1, 0, 0, 20),
    Position = UDim2.new(0, 0, 0, 72),
    BackgroundTransparency = 1,
    Text = "SISTEMA DE AUTENTICAÇÃO",
    TextColor3 = CONFIG.COR_SUBTEXTO,
    Font = CONFIG.FONTE,
    TextSize = 11,
    Parent = KeyScreen,
})

local keyBox = criar("TextBox", {
    Size = UDim2.new(0, 260, 0, 46),
    Position = UDim2.new(0.5, -130, 0, 110),
    BackgroundColor3 = CONFIG.COR_FUNDO,
    BorderSizePixel = 0,
    Text = "",
    PlaceholderText = "Digite sua Key...",
    PlaceholderColor3 = CONFIG.COR_SUBTEXTO,
    TextColor3 = CONFIG.COR_TEXTO,
    Font = CONFIG.FONTE,
    TextSize = 15,
    Parent = KeyScreen,
    ClearTextOnFocus = false,
})
arredondar(keyBox, 10)
local keyStroke = criar("UIStroke", {
    Color = CONFIG.COR_PRIMARIA,
    Thickness = 1,
    Transparency = 0.6,
    Parent = keyBox,
})
criar("UIPadding", {
    PaddingLeft = UDim.new(0, 14),
    PaddingRight = UDim.new(0, 14),
    Parent = keyBox,
})

local confirmBtn = criar("TextButton", {
    Size = UDim2.new(0, 260, 0, 46),
    Position = UDim2.new(0.5, -130, 0, 175),
    BackgroundColor3 = CONFIG.COR_PRIMARIA,
    BorderSizePixel = 0,
    Text = "CONFIRMAR",
    TextColor3 = Color3.fromRGB(255, 255, 255),
    Font = CONFIG.FONTE_BOLD,
    TextSize = 15,
    Parent = KeyScreen,
    AutoButtonColor = false,
})
arredondar(confirmBtn, 10)
gradiente(confirmBtn, CONFIG.COR_PRIMARIA, CONFIG.COR_SECUNDARIA, 0)

local errorLabel = criar("TextLabel", {
    Size = UDim2.new(1, 0, 0, 18),
    Position = UDim2.new(0, 0, 1, -22),
    BackgroundTransparency = 1,
    Text = "",
    TextColor3 = Color3.fromRGB(255, 80, 80),
    Font = CONFIG.FONTE,
    TextSize = 12,
    Parent = KeyScreen,
})

confirmBtn.MouseEnter:Connect(function()
    TweenService:Create(confirmBtn, TweenInfo.new(0.2), {BackgroundColor3 = CONFIG.COR_SECUNDARIA}):Play()
end)
confirmBtn.MouseLeave:Connect(function()
    TweenService:Create(confirmBtn, TweenInfo.new(0.2), {BackgroundColor3 = CONFIG.COR_PRIMARIA}):Play()
end)

--// HUB PRINCIPAL
local Hub = criar("Frame", {
    Size = UDim2.new(0, 340, 0, 420),
    Position = UDim2.new(0.5, -170, 0.5, -210),
    BackgroundColor3 = CONFIG.COR_PAINEL,
    BorderSizePixel = 0,
    Parent = ScreenGui,
    Visible = false,
    ClipsDescendants = true,
    Active = true,
})
arredondar(Hub, 14)
gradiente(Hub, CONFIG.COR_PAINEL, CONFIG.COR_FUNDO, 135)
sombra(Hub)

local hubTopBar = criar("Frame", {
    Size = UDim2.new(1, 0, 0, 42),
    BackgroundColor3 = CONFIG.COR_FUNDO,
    BorderSizePixel = 0,
    Parent = Hub,
})
arredondar(hubTopBar, 14)
criar("Frame", {
    Size = UDim2.new(1, 0, 0.5, 0),
    Position = UDim2.new(0, 0, 0.5, 0),
    BackgroundColor3 = CONFIG.COR_FUNDO,
    BorderSizePixel = 0,
    Parent = hubTopBar,
})

local hubTitle = criar("TextLabel", {
    Size = UDim2.new(0, 200, 1, 0),
    Position = UDim2.new(0, 14, 0, 0),
    BackgroundTransparency = 1,
    Text = "PAK HUB V2",
    TextColor3 = CONFIG.COR_TEXTO,
    Font = CONFIG.FONTE_BOLD,
    TextSize = 16,
    TextXAlignment = Enum.TextXAlignment.Left,
    Parent = hubTopBar,
})
gradiente(hubTitle, CONFIG.COR_PRIMARIA, CONFIG.COR_SECUNDARIA, 0)

local minimBtn = criar("TextButton", {
    Size = UDim2.new(0, 30, 0, 30),
    Position = UDim2.new(1, -74, 0.5, -15),
    BackgroundColor3 = CONFIG.COR_PAINEL,
    BorderSizePixel = 0,
    Text = "−",
    TextColor3 = CONFIG.COR_TEXTO,
    Font = CONFIG.FONTE_BOLD,
    TextSize = 20,
    Parent = hubTopBar,
    AutoButtonColor = false,
})
arredondar(minimBtn, 8)

local closeBtn = criar("TextButton", {
    Size = UDim2.new(0, 30, 0, 30),
    Position = UDim2.new(1, -38, 0.5, -15),
    BackgroundColor3 = CONFIG.COR_PAINEL,
    BorderSizePixel = 0,
    Text = "×",
    TextColor3 = CONFIG.COR_TEXTO,
    Font = CONFIG.FONTE_BOLD,
    TextSize = 20,
    Parent = hubTopBar,
    AutoButtonColor = false,
})
arredondar(closeBtn, 8)

minimBtn.MouseEnter:Connect(function() minimBtn.BackgroundColor3 = CONFIG.COR_PRIMARIA end)
minimBtn.MouseLeave:Connect(function() minimBtn.BackgroundColor3 = CONFIG.COR_PAINEL end)
closeBtn.MouseEnter:Connect(function() closeBtn.BackgroundColor3 = Color3.fromRGB(200, 40, 40) end)
closeBtn.MouseLeave:Connect(function() closeBtn.BackgroundColor3 = CONFIG.COR_PAINEL end)

local FloatingBall = criar("TextButton", {
    Size = UDim2.new(0, 50, 0, 50),
    Position = UDim2.new(0, 20, 0.5, -25),
    BackgroundColor3 = CONFIG.COR_PRIMARIA,
    BorderSizePixel = 0,
    Text = "P",
    TextColor3 = Color3.fromRGB(255, 255, 255),
    Font = CONFIG.FONTE_BOLD,
    TextSize = 20,
    Parent = ScreenGui,
    Visible = false,
    AutoButtonColor = false,
})
arredondar(FloatingBall, 25)
gradiente(FloatingBall, CONFIG.COR_PRIMARIA, CONFIG.COR_SECUNDARIA, 45)
sombra(FloatingBall)

local ScrollFrame = criar("ScrollingFrame", {
    Size = UDim2.new(1, -20, 1, -60),
    Position = UDim2.new(0, 10, 0, 50),
    BackgroundTransparency = 1,
    BorderSizePixel = 0,
    ScrollBarThickness = 3,
    ScrollBarImageColor3 = CONFIG.COR_PRIMARIA,
    CanvasSize = UDim2.new(0, 0, 0, 0),
    Parent = Hub,
})
local scrollLayout = criar("UIListLayout", {
    Padding = UDim.new(0, 8),
    SortOrder = Enum.SortOrder.LayoutOrder,
    Parent = ScrollFrame,
})

-- FIM DA PARTE 1
                            --// FUNÇÃO CATEGORIA
local function criarCategoria(nome, ordem)
    local catFrame = criar("Frame", {
        Size = UDim2.new(1, -6, 0, 36),
        BackgroundColor3 = CONFIG.COR_FUNDO,
        BorderSizePixel = 0,
        LayoutOrder = ordem,
        Parent = ScrollFrame,
    })
    arredondar(catFrame, 8)
    criar("UIStroke", {
        Color = CONFIG.COR_PRIMARIA,
        Thickness = 1,
        Transparency = 0.7,
        Parent = catFrame,
    })
    criar("TextLabel", {
        Size = UDim2.new(1, 0, 1, 0),
        BackgroundTransparency = 1,
        Text = "▸ " .. nome,
        TextColor3 = CONFIG.COR_PRIMARIA,
        Font = CONFIG.FONTE_BOLD,
        TextSize = 13,
        TextXAlignment = Enum.TextXAlignment.Left,
        Parent = catFrame,
    })
    criar("UIPadding", {
        PaddingLeft = UDim.new(0, 12),
        Parent = catFrame,
    })
    return catFrame
end

--// FUNÇÃO TOGGLE
local function criarToggle(nome, ordem, callback)
    local container = criar("Frame", {
        Size = UDim2.new(1, -6, 0, 34),
        BackgroundColor3 = CONFIG.COR_PAINEL,
        BorderSizePixel = 0,
        LayoutOrder = ordem,
        Parent = ScrollFrame,
    })
    arredondar(container, 8)

    criar("TextLabel", {
        Size = UDim2.new(0.7, 0, 1, 0),
        Position = UDim2.new(0, 12, 0, 0),
        BackgroundTransparency = 1,
        Text = nome,
        TextColor3 = CONFIG.COR_TEXTO,
        Font = CONFIG.FONTE,
        TextSize = 12,
        TextXAlignment = Enum.TextXAlignment.Left,
        Parent = container,
    })

    local toggleBg = criar("Frame", {
        Size = UDim2.new(0, 40, 0, 20),
        Position = UDim2.new(1, -52, 0.5, -10),
        BackgroundColor3 = Color3.fromRGB(60, 55, 75),
        BorderSizePixel = 0,
        Parent = container,
    })
    arredondar(toggleBg, 10)

    local circle = criar("Frame", {
        Size = UDim2.new(0, 16, 0, 16),
        Position = UDim2.new(0, 2, 0.5, -8),
        BackgroundColor3 = Color3.fromRGB(255, 255, 255),
        BorderSizePixel = 0,
        Parent = toggleBg,
    })
    arredondar(circle, 8)

    local ativo = false
    local btn = criar("TextButton", {
        Size = UDim2.new(1, 0, 1, 0),
        BackgroundTransparency = 1,
        Text = "",
        Parent = container,
    })

    btn.MouseButton1Click:Connect(function()
        ativo = not ativo
        if ativo then
            TweenService:Create(toggleBg, TweenInfo.new(0.2), {BackgroundColor3 = CONFIG.COR_PRIMARIA}):Play()
            TweenService:Create(circle, TweenInfo.new(0.2), {Position = UDim2.new(1, -18, 0.5, -8)}):Play()
        else
            TweenService:Create(toggleBg, TweenInfo.new(0.2), {BackgroundColor3 = Color3.fromRGB(60, 55, 75)}):Play()
            TweenService:Create(circle, TweenInfo.new(0.2), {Position = UDim2.new(0, 2, 0.5, -8)}):Play()
        end
        if callback then callback(ativo) end
    end)

    return container
end

--// FUNÇÃO SLIDER
local function criarSlider(nome, ordem, min, max, padrao, callback)
    local container = criar("Frame", {
        Size = UDim2.new(1, -6, 0, 50),
        BackgroundColor3 = CONFIG.COR_PAINEL,
        BorderSizePixel = 0,
        LayoutOrder = ordem,
        Parent = ScrollFrame,
    })
    arredondar(container, 8)

    criar("TextLabel", {
        Size = UDim2.new(0.7, 0, 0, 18),
        Position = UDim2.new(0, 12, 0, 4),
        BackgroundTransparency = 1,
        Text = nome,
        TextColor3 = CONFIG.COR_TEXTO,
        Font = CONFIG.FONTE,
        TextSize = 12,
        TextXAlignment = Enum.TextXAlignment.Left,
        Parent = container,
    })

    local valorLabel = criar("TextLabel", {
        Size = UDim2.new(0.25, 0, 0, 18),
        Position = UDim2.new(0.7, 0, 0, 4),
        BackgroundTransparency = 1,
        Text = tostring(padrao),
        TextColor3 = CONFIG.COR_PRIMARIA,
        Font = CONFIG.FONTE_BOLD,
        TextSize = 12,
        TextXAlignment = Enum.TextXAlignment.Right,
        Parent = container,
    })

    local barBg = criar("Frame", {
        Size = UDim2.new(1, -24, 0, 6),
        Position = UDim2.new(0, 12, 0, 32),
        BackgroundColor3 = CONFIG.COR_FUNDO,
        BorderSizePixel = 0,
        Parent = container,
    })
    arredondar(barBg, 3)

    local fill = criar("Frame", {
        Size = UDim2.new((padrao - min) / (max - min), 0, 1, 0),
        BackgroundColor3 = CONFIG.COR_PRIMARIA,
        BorderSizePixel = 0,
        Parent = barBg,
    })
    arredondar(fill, 3)
    gradiente(fill, CONFIG.COR_PRIMARIA, CONFIG.COR_SECUNDARIA, 0)

    local knob = criar("Frame", {
        Size = UDim2.new(0, 14, 0, 14),
        Position = UDim2.new((padrao - min) / (max - min), -7, 0.5, -7),
        BackgroundColor3 = Color3.fromRGB(255, 255, 255),
        BorderSizePixel = 0,
        Parent = barBg,
        ZIndex = 2,
    })
    arredondar(knob, 7)

    local dragging = false
    local btn = criar("TextButton", {
        Size = UDim2.new(1, 0, 1, 0),
        BackgroundTransparency = 1,
        Text = "",
        Parent = barBg,
        ZIndex = 3,
    })

    local function update(input)
        local pos = math.clamp((input.Position.X - barBg.AbsolutePosition.X) / barBg.AbsoluteSize.X, 0, 1)
        local val = math.floor(min + (max - min) * pos)
        valorLabel.Text = tostring(val)
        TweenService:Create(fill, TweenInfo.new(0.05), {Size = UDim2.new(pos, 0, 1, 0)}):Play()
        TweenService:Create(knob, TweenInfo.new(0.05), {Position = UDim2.new(pos, -7, 0.5, -7)}):Play()
        if callback then callback(val) end
    end

    btn.InputBegan:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
            dragging = true
            update(input)
        end
    end)
    btn.InputChanged:Connect(function(input)
        if dragging and (input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch) then
            update(input)
        end
    end)
    UserInputService.InputEnded:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
            dragging = false
        end
    end)

    return container
end

--// FUNÇÃO BOTÃO
local function criarBotao(nome, ordem, callback)
    local btn = criar("TextButton", {
        Size = UDim2.new(1, -6, 0, 36),
        BackgroundColor3 = CONFIG.COR_PAINEL,
        BorderSizePixel = 0,
        Text = nome,
        TextColor3 = CONFIG.COR_TEXTO,
        Font = CONFIG.FONTE,
        TextSize = 12,
        LayoutOrder = ordem,
        Parent = ScrollFrame,
        AutoButtonColor = false,
    })
    arredondar(btn, 8)
    criar("UIStroke", {
        Color = CONFIG.COR_PRIMARIA,
        Thickness = 1,
        Transparency = 0.7,
        Parent = btn,
    })

    btn.MouseEnter:Connect(function()
        TweenService:Create(btn, TweenInfo.new(0.2), {BackgroundColor3 = CONFIG.COR_PRIMARIA}):Play()
    end)
    btn.MouseLeave:Connect(function()
        TweenService:Create(btn, TweenInfo.new(0.2), {BackgroundColor3 = CONFIG.COR_PAINEL}):Play()
    end)
    btn.MouseButton1Click:Connect(function()
        if callback then callback() end
    end)

    return btn
end

--// CONSTRUÇÃO DO HUB
local ordem = 1

criarCategoria("COMBAT", ordem); ordem = ordem + 1
criarToggle("Aimbot", ordem, function(v) State.Aimbot = v end); ordem = ordem + 1
criarSlider("Aimbot FOV", ordem, 30, 500, 120, function(v) State.AimbotFOV = v end); ordem = ordem + 1

criarCategoria("VISUALS", ordem); ordem = ordem + 1
criarToggle("ESP", ordem, function(v) State.ESP = v end); ordem = ordem + 1
criarToggle("Box", ordem, function(v) State.Box = v end); ordem = ordem + 1
criarToggle("Lines", ordem, function(v) State.Lines = v end); ordem = ordem + 1
criarToggle("Name", ordem, function(v) State.Name = v end); ordem = ordem + 1
criarToggle("Distance", ordem, function(v) State.Distance = v end); ordem = ordem + 1
criarToggle("Health", ordem, function(v) State.Health = v end); ordem = ordem + 1

criarCategoria("MOVEMENT", ordem); ordem = ordem + 1
criarToggle("Speed", ordem, function(v) State.Speed = v end); ordem = ordem + 1
criarSlider("Speed Value", ordem, 16, 200, 25, function(v) State.SpeedValue = v end); ordem = ordem + 1
criarToggle("Noclip", ordem, function(v) State.Noclip = v end); ordem = ordem + 1
criarToggle("Spinbot", ordem, function(v) State.Spinbot = v end); ordem = ordem + 1
criarSlider("Spin Speed", ordem, 1, 50, 10, function(v) State.SpinSpeed = v end); ordem = ordem + 1
            criarBotao("★ Créditos", ordem, function()
    local creditos = ScreenGui:FindFirstChild("Creditos")
    if creditos then creditos:Destroy() return end

    local credFrame = criar("Frame", {
        Size = UDim2.new(0, 260, 0, 200),
        Position = UDim2.new(0.5, -130, 0.5, -100),
        BackgroundColor3 = CONFIG.COR_PAINEL,
        BorderSizePixel = 0,
        Parent = ScreenGui,
        Name = "Creditos",
        ZIndex = 10,
    })
    arredondar(credFrame, 14)
    gradiente(credFrame, CONFIG.COR_PAINEL, CONFIG.COR_FUNDO, 135)
    sombra(credFrame)

    local avatar = criar("ImageLabel", {
        Size = UDim2.new(0, 70, 0, 70),
        Position = UDim2.new(0.5, -35, 0, 20),
        BackgroundColor3 = CONFIG.COR_FUNDO,
        BorderSizePixel = 0,
        Parent = credFrame,
        ZIndex = 11,
    })
    arredondar(avatar, 35)

    pcall(function()
        local id = Players:GetUserIdFromNameAsync(CONFIG.CRIADOR)
        local thumb = Players:GetUserThumbnailAsync(id, Enum.ThumbnailType.HeadShot, Enum.ThumbnailSize.Size150x150)
        avatar.Image = thumb
    end)

    criar("TextLabel", {
        Size = UDim2.new(1, 0, 0, 25),
        Position = UDim2.new(0, 0, 0, 100),
        BackgroundTransparency = 1,
        Text = CONFIG.CRIADOR,
        TextColor3 = CONFIG.COR_TEXTO,
        Font = CONFIG.FONTE_BOLD,
        TextSize = 16,
        Parent = credFrame,
        ZIndex = 11,
    })
    criar("TextLabel", {
        Size = UDim2.new(1, 0, 0, 20),
        Position = UDim2.new(0, 0, 0, 125),
        BackgroundTransparency = 1,
        Text = "Criador do PAK HUB V2",
        TextColor3 = CONFIG.COR_SUBTEXTO,
        Font = CONFIG.FONTE,
        TextSize = 11,
        Parent = credFrame,
        ZIndex = 11,
    })
    criar("TextLabel", {
        Size = UDim2.new(1, 0, 0, 25),
        Position = UDim2.new(0, 0, 0, 155),
        BackgroundTransparency = 1,
        Text = "Obrigado por usar!",
        TextColor3 = CONFIG.COR_PRIMARIA,
        Font = CONFIG.FONTE_BOLD,
        TextSize = 13,
        Parent = credFrame,
        ZIndex = 11,
    })

    local fechar = criar("TextButton", {
        Size = UDim2.new(0, 30, 0, 30),
        Position = UDim2.new(1, -38, 0, 8),
        BackgroundColor3 = CONFIG.COR_FUNDO,
        BorderSizePixel = 0,
        Text = "×",
        TextColor3 = CONFIG.COR_TEXTO,
        Font = CONFIG.FONTE_BOLD,
        TextSize = 18,
        Parent = credFrame,
        ZIndex = 12,
    })
    arredondar(fechar, 8)
    fechar.MouseButton1Click:Connect(function() credFrame:Destroy() end)
end); ordem = ordem + 1

scrollLayout:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(function()
    ScrollFrame.CanvasSize = UDim2.new(0, 0, 0, scrollLayout.AbsoluteContentSize.Y + 20)
end)

--// MENSAGEM DE BOAS-VINDAS
local function mostrarBoasVindas()
    local welcome = criar("Frame", {
        Size = UDim2.new(0, 300, 0, 70),
        Position = UDim2.new(0.5, -150, 0, -80),
        BackgroundColor3 = CONFIG.COR_PAINEL,
        BorderSizePixel = 0,
        Parent = ScreenGui,
        ZIndex = 20,
    })
    arredondar(welcome, 12)
    gradiente(welcome, CONFIG.COR_PAINEL, CONFIG.COR_FUNDO, 135)
    sombra(welcome)

    criar("TextLabel", {
        Size = UDim2.new(1, 0, 0, 30),
        Position = UDim2.new(0, 0, 0, 8),
        BackgroundTransparency = 1,
        Text = "Quem não xita, não brilha",
        TextColor3 = CONFIG.COR_PRIMARIA,
        Font = CONFIG.FONTE_BOLD,
        TextSize = 15,
        Parent = welcome,
        ZIndex = 21,
    })
    criar("TextLabel", {
        Size = UDim2.new(1, 0, 0, 25),
        Position = UDim2.new(0, 0, 0, 36),
        BackgroundTransparency = 1,
        Text = "Bem-vindo, " .. LocalPlayer.Name .. "!",
        TextColor3 = CONFIG.COR_TEXTO,
        Font = CONFIG.FONTE,
        TextSize = 13,
        Parent = welcome,
        ZIndex = 21,
    })

    TweenService:Create(welcome, TweenInfo.new(0.5, Enum.EasingStyle.Back, Enum.EasingDirection.Out), {
        Position = UDim2.new(0.5, -150, 0, 20)
    }):Play()

    task.wait(3.5)
    local out = TweenService:Create(welcome, TweenInfo.new(0.5, Enum.EasingStyle.Quad, Enum.EasingDirection.In), {
        Position = UDim2.new(0.5, -150, 0, -80),
        BackgroundTransparency = 1
    })
    out:Play()
    for _, v in pairs(welcome:GetDescendants()) do
        if v:IsA("TextLabel") then
            TweenService:Create(v, TweenInfo.new(0.5), {TextTransparency = 1}):Play()
        end
    end
    out.Completed:Connect(function() welcome:Destroy() end)
end

--// DRAG
local function makeDraggable(frame, handle)
    local dragging, dragStart, startPos
    handle = handle or frame

    handle.InputBegan:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
            dragging = true
            dragStart = input.Position
            startPos = frame.Position
            input.Changed:Connect(function()
                if input.UserInputState == Enum.UserInputState.End then
                    dragging = false
                end
            end)
        end
    end)

    handle.InputChanged:Connect(function(input)
        if dragging and (input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch) then
            local delta = input.Position - dragStart
            frame.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
        end
    end)
end

makeDraggable(Hub, hubTopBar)
makeDraggable(KeyScreen, KeyScreen)
makeDraggable(FloatingBall)

--// VERIFICAÇÃO DA KEY
confirmBtn.MouseButton1Click:Connect(function()
    if keyBox.Text == CONFIG.KEY_CORRETA then
        local out = TweenService:Create(KeyScreen, TweenInfo.new(0.4, Enum.EasingStyle.Back, Enum.EasingDirection.In), {
            Position = UDim2.new(0.5, -170, 0.5, 400),
            BackgroundTransparency = 1
        })
        out:Play()
        for _, v in pairs(KeyScreen:GetDescendants()) do
            if v:IsA("TextLabel") or v:IsA("TextButton") or v:IsA("TextBox") then
                TweenService:Create(v, TweenInfo.new(0.4), {TextTransparency = 1, BackgroundTransparency = 1}):Play()
            end
        end
        out.Completed:Connect(function()
            KeyScreen:Destroy()
            Hub.Visible = true
            Hub.Position = UDim2.new(0.5, -170, 0.5, 300)
            TweenService:Create(Hub, TweenInfo.new(0.5, Enum.EasingStyle.Back, Enum.EasingDirection.Out), {
                Position = UDim2.new(0.5, -170, 0.5, -210)
            }):Play()
            mostrarBoasVindas()
        end)
    else
        errorLabel.Text = "✗ Key inválida. Tente novamente."
        keyStroke.Color = Color3.fromRGB(255, 60, 60)
        TweenService:Create(keyBox, TweenInfo.new(0.1), {Position = UDim2.new(0.5, -135, 0, 110)}):Play()
        task.wait(0.1)
        TweenService:Create(keyBox, TweenInfo.new(0.1), {Position = UDim2.new(0.5, -125, 0, 110)}):Play()
        task.wait(0.1)
        TweenService:Create(keyBox, TweenInfo.new(0.1), {Position = UDim2.new(0.5, -130, 0, 110)}):Play()
        task.wait(0.5)
        keyStroke.Color = CONFIG.COR_PRIMARIA
        errorLabel.Text = ""
    end
end)

--// MINIMIZAR / RESTAURAR
minimBtn.MouseButton1Click:Connect(function()
    Hub.Visible = false
    FloatingBall.Visible = true
end)

FloatingBall.MouseButton1Click:Connect(function()
    FloatingBall.Visible = false
    Hub.Visible = true
end)

--// FECHAR
closeBtn.MouseButton1Click:Connect(function()
    Hub.Visible = false
    FloatingBall.Visible = true
    local confirm = criar("Frame", {
        Size = UDim2.new(0, 220, 0, 100),
        Position = UDim2.new(0.5, -110, 0.5, -50),
        BackgroundColor3 = CONFIG.COR_PAINEL,
        BorderSizePixel = 0,
        Parent = ScreenGui,
        ZIndex = 30,
    })
    arredondar(confirm, 12)
    sombra(confirm)

    criar("TextLabel", {
        Size = UDim2.new(1, 0, 0, 35),
        Position = UDim2.new(0, 0, 0, 8),
        BackgroundTransparency = 1,
        Text = "Deseja realmente fechar?",
        TextColor3 = CONFIG.COR_TEXTO,
        Font = CONFIG.FONTE,
        TextSize = 13,
        Parent = confirm,
        ZIndex = 31,
    })

    local sim = criar("TextButton", {
        Size = UDim2.new(0, 90, 0, 32),
        Position = UDim2.new(0, 15, 0, 55),
        BackgroundColor3 = Color3.fromRGB(200, 40, 40),
        BorderSizePixel = 0,
        Text = "SIM",
        TextColor3 = Color3.fromRGB(255, 255, 255),
        Font = CONFIG.FONTE_BOLD,
        TextSize = 12,
        Parent = confirm,
        ZIndex = 31,
    })
    arredondar(sim, 8)

    local nao = criar("TextButton", {
        Size = UDim2.new(0, 90, 0, 32),
        Position = UDim2.new(1, -105, 0, 55),
        BackgroundColor3 = CONFIG.COR_PRIMARIA,
        BorderSizePixel = 0,
        Text = "NÃO",
        TextColor3 = Color3.fromRGB(255, 255, 255),
        Font = CONFIG.FONTE_BOLD,
        TextSize = 12,
        Parent = confirm,
        ZIndex = 31,
    })
    arredondar(nao, 8)

    sim.MouseButton1Click:Connect(function()
        ScreenGui:Destroy()
    end)
    nao.MouseButton1Click:Connect(function()
        confirm:Destroy()
    end)
end)--// MÓDULO ESP
local espObjects = {}

local function criarESP(player)
    if player == LocalPlayer then return end
    if espObjects[player] then return end

    local box = Drawing.new("Square")
    box.Thickness = 1.5
    box.Color = CONFIG.COR_PRIMARIA
    box.Filled = false
    box.Transparency = 1
    box.Visible = false

    local nameTag = Drawing.new("Text")
    nameTag.Size = 14
    nameTag.Center = true
    nameTag.Outline = true
    nameTag.Color = Color3.fromRGB(255, 255, 255)
    nameTag.Visible = false

    local distTag = Drawing.new("Text")
    distTag.Size = 12
    distTag.Center = true
    distTag.Outline = true
    distTag.Color = Color3.fromRGB(200, 200, 200)
    distTag.Visible = false

    local healthBar = Drawing.new("Line")
    healthBar.Thickness = 2
    healthBar.Color = Color3.fromRGB(0, 255, 0)
    healthBar.Visible = false

    local line = Drawing.new("Line")
    line.Thickness = 1
    line.Color = CONFIG.COR_PRIMARIA
    line.Visible = false

    espObjects[player] = {
        box = box, name = nameTag, dist = distTag,
        health = healthBar, line = line
    }
end

local function removerESP(player)
    if espObjects[player] then
        for _, obj in pairs(espObjects[player]) do
            pcall(function() obj:Remove() end)
        end
        espObjects[player] = nil
    end
end

Players.PlayerAdded:Connect(criarESP)
Players.PlayerRemoving:Connect(removerESP)
for _, p in pairs(Players:GetPlayers()) do criarESP(p) end

--// FOV CIRCLE
local fovCircle = Drawing.new("Circle")
fovCircle.Thickness = 1.5
fovCircle.Color = CONFIG.COR_PRIMARIA
fovCircle.Filled = false
fovCircle.Transparency = 0.7
fovCircle.NumSides = 60
fovCircle.Radius = State.AimbotFOV
fovCircle.Visible = false

--// LOOP PRINCIPAL
RunService.RenderStepped:Connect(function()
    if State.Aimbot then
        fovCircle.Visible = true
        fovCircle.Radius = State.AimbotFOV
        fovCircle.Position = Vector2.new(Mouse.X, Mouse.Y)
    else
        fovCircle.Visible = false
    end

    for player, obj in pairs(espObjects) do
        local char = player.Character
        if char and char:FindFirstChild("HumanoidRootPart") and char:FindFirstChild("Humanoid") then
            local hrp = char.HumanoidRootPart
            local hum = char.Humanoid
            local pos, onScreen = Camera:WorldToViewportPoint(hrp.Position)

            if onScreen and State.ESP then
                local head = char:FindFirstChild("Head")
                if head then
                    local headPos = Camera:WorldToViewportPoint(head.Position + Vector3.new(0, 0.5, 0))
                    local footPos = Camera:WorldToViewportPoint(hrp.Position - Vector3.new(0, 3, 0))
                    local height = math.abs(headPos.Y - footPos.Y)
                    local width = height / 2

                    if State.Box then
                        obj.box.Visible = true
                        obj.box.Size = Vector2.new(width, height)
                        obj.box.Position = Vector2.new(pos.X - width/2, pos.Y - height/2)
                    else
                        obj.box.Visible = false
                    end

                    if State.Name then
                        obj.name.Visible = true
                        obj.name.Text = player.Name
                        obj.name.Position = Vector2.new(pos.X, pos.Y - height/2 - 18)
                    else
                        obj.name.Visible = false
                    end

                    if State.Distance then
                        obj.dist.Visible = true
                        local dist = math.floor((hrp.Position - Camera.CFrame.Position).Magnitude)
                        obj.dist.Text = tostring(dist) .. "m"
                        obj.dist.Position = Vector2.new(pos.X, pos.Y + height/2 + 4)
                    else
                        obj.dist.Visible = false
                    end

                    if State.Health then
                        obj.health.Visible = true
                        local hp = hum.Health / hum.MaxHealth
                        local barX = pos.X - width/2 - 8
                        obj.health.From = Vector2.new(barX, pos.Y + height/2)
                        obj.health.To = Vector2.new(barX, pos.Y + height/2 - (height * hp))
                        obj.health.Color = Color3.fromRGB(255 * (1 - hp), 255 * hp, 0)
                    else
                        obj.health.Visible = false
                    end

                    if State.Lines then
                        obj.line.Visible = true
                        obj.line.From = Vector2.new(Camera.ViewportSize.X / 2, Camera.ViewportSize.Y)
                        obj.line.To = Vector2.new(pos.X, pos.Y + height/2)
                    else
                        obj.line.Visible = false
                    end
                end
            else
                obj.box.Visible = false
                obj.name.Visible = false
                obj.dist.Visible = false
                obj.health.Visible = false
                obj.line.Visible = false
            end
        end
    end

    if State.Aimbot then
        local closest, closestDist = nil, State.AimbotFOV
        for _, player in pairs(Players:GetPlayers()) do
            if player ~= LocalPlayer and player.Character and player.Character:FindFirstChild("Head") then
                local head = player.Character.Head
                local pos, onScreen = Camera:WorldToViewportPoint(head.Position)
                if onScreen then
                    local dist = (Vector2.new(pos.X, pos.Y) - Vector2.new(Mouse.X, Mouse.Y)).Magnitude
                    if dist < closestDist then
                        closestDist = dist
                        closest = head
                    end
                end
            end
        end
        if closest then
            Camera.CFrame = CFrame.new(Camera.CFrame.Position, closest.Position)
        end
    end

    if State.Speed then
        local char = LocalPlayer.Character
        if char and char:FindFirstChild("Humanoid") then
            char.Humanoid.WalkSpeed = State.SpeedValue
        end
    end

    if State.Noclip then
        local char = LocalPlayer.Character
        if char then
            for _, v in pairs(char:GetDescendants()) do
                if v:IsA("BasePart") and v.CanCollide then
                    v.CanCollide = false
                end
            end
        end
    end

    if State.Spinbot then
        local char = LocalPlayer.Character
        if char and char:FindFirstChild("HumanoidRootPart") then
            char.HumanoidRootPart.CFrame = char.HumanoidRootPart.CFrame * CFrame.Angles(0, math.rad(State.SpinSpeed), 0)
        end
    end
end)

StarterGui:SetCore("SendNotification", {
    Title = "PAK HUB V2",
    Text = "Script carregado!",
    Duration = 3,
})
