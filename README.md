-- LocalScript (coloque dentro de StarterPlayerScripts)

local player = game.Players.LocalPlayer
local mouse = player:GetMouse()
local markedPosition = nil

-- UI Setup
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "TeleGuiadoUI"
screenGui.Parent = player:WaitForChild("PlayerGui")

local mainFrame = Instance.new("Frame")
mainFrame.Size = UDim2.new(0, 300, 0, 180)
mainFrame.Position = UDim2.new(0.5, -150, 0.8, -90)
mainFrame.BackgroundColor3 = Color3.fromRGB(40,40,60)
mainFrame.BorderSizePixel = 0
mainFrame.AnchorPoint = Vector2.new(0.5,0.5)
mainFrame.Parent = screenGui
mainFrame.Active = true
mainFrame.Draggable = true

local title = Instance.new("TextLabel")
title.Size = UDim2.new(1, 0, 0, 40)
title.BackgroundTransparency = 1
title.Text = "TeleGuiado"
title.Font = Enum.Font.GothamBold
title.TextSize = 28
title.TextColor3 = Color3.fromRGB(150,200,255)
title.Parent = mainFrame

local info = Instance.new("TextLabel")
info.Position = UDim2.new(0, 0, 0, 40)
info.Size = UDim2.new(1, 0, 0, 30)
info.BackgroundTransparency = 1
info.Text = "Marque uma posição para se teleportar!"
info.Font = Enum.Font.Gotham
info.TextSize = 17
info.TextColor3 = Color3.fromRGB(200,200,200)
info.Parent = mainFrame

local actionButton = Instance.new("TextButton")
actionButton.Size = UDim2.new(0.8, 0, 0, 50)
actionButton.Position = UDim2.new(0.1, 0, 0.5, 0)
actionButton.BackgroundColor3 = Color3.fromRGB(60,120,200)
actionButton.Text = "Marcar Posição"
actionButton.Font = Enum.Font.GothamBold
actionButton.TextSize = 22
actionButton.TextColor3 = Color3.fromRGB(255,255,255)
actionButton.Parent = mainFrame
actionButton.BorderSizePixel = 0
actionButton.AutoButtonColor = true

-- Button Functionality
actionButton.MouseButton1Click:Connect(function()
    if not markedPosition then
        -- Marcar posição
        local char = player.Character or player.CharacterAdded:Wait()
        if char:FindFirstChild("HumanoidRootPart") then
            markedPosition = char.HumanoidRootPart.Position
            actionButton.Text = "Teleguiado"
            info.Text = "Clique para ir até a posição marcada!"
            actionButton.BackgroundColor3 = Color3.fromRGB(60,200,120)
        end
    else
        -- Teleguiado (teleportar)
        local char = player.Character or player.CharacterAdded:Wait()
        if char:FindFirstChild("HumanoidRootPart") then
            char.HumanoidRootPart.CFrame = CFrame.new(markedPosition)
            info.Text = "Você foi teleguiado!"
        end
    end
end)

-- Opcional: Botão para Resetar a posição marcada
local resetButton = Instance.new("TextButton")
resetButton.Size = UDim2.new(0.4, 0, 0, 30)
resetButton.Position = UDim2.new(0.3, 0, 0.8, 0)
resetButton.BackgroundColor3 = Color3.fromRGB(200,60,60)
resetButton.Text = "Resetar Posição"
resetButton.Font = Enum.Font.Gotham
resetButton.TextSize = 15
resetButton.TextColor3 = Color3.fromRGB(255,255,255)
resetButton.Parent = mainFrame
resetButton.BorderSizePixel = 0
resetButton.AutoButtonColor = true

resetButton.MouseButton1Click:Connect(function()
    markedPosition = nil
    actionButton.Text = "Marcar Posição"
    info.Text = "Marque uma posição para se teleportar!"
    actionButton.BackgroundColor3 = Color3.fromRGB(60,120,200)
end)
