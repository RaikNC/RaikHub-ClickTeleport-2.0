-- Criação do Menu
local ScreenGui = Instance.new("ScreenGui")
local MainFrame = Instance.new("Frame")
local CloseButton = Instance.new("TextButton")
local ClickTPButton = Instance.new("TextButton")
local DuplicateButton = Instance.new("TextButton")
local OpenButton = Instance.new("TextButton")

-- Propriedades do ScreenGui
ScreenGui.Name = "MenuGui"
ScreenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")

-- Propriedades do MainFrame
MainFrame.Name = "MainFrame"
MainFrame.Parent = ScreenGui
MainFrame.BackgroundColor3 = Color3.new(1, 1, 1)
MainFrame.Size = UDim2.new(0, 300, 0, 200)
MainFrame.Position = UDim2.new(0.5, -150, 0.5, -100)

-- Propriedades do CloseButton
CloseButton.Name = "CloseButton"
CloseButton.Parent = MainFrame
CloseButton.Text = "X"
CloseButton.Size = UDim2.new(0, 50, 0, 50)
CloseButton.Position = UDim2.new(1, -60, 0, 10)

-- Propriedades do ClickTPButton
ClickTPButton.Name = "ClickTPButton"
ClickTPButton.Parent = MainFrame
ClickTPButton.Text = "ClickTP - OFF"
ClickTPButton.Size = UDim2.new(0, 200, 0, 50)
ClickTPButton.Position = UDim2.new(0.5, -100, 0.5, -25)

-- Propriedades do DuplicateButton
DuplicateButton.Name = "DuplicateButton"
DuplicateButton.Parent = MainFrame
DuplicateButton.Text = "Duplicate Item"
DuplicateButton.Size = UDim2.new(0, 200, 0, 50)
DuplicateButton.Position = UDim2.new(0.5, -100, 0.5, 35)

-- Propriedades do OpenButton
OpenButton.Name = "OpenButton"
OpenButton.Parent = ScreenGui
OpenButton.Text = "Open Menu"
OpenButton.Size = UDim2.new(0, 100, 0, 50)
OpenButton.Position = UDim2.new(0, 10, 0, 10)
OpenButton.Visible = false

-- Função para fechar o menu
CloseButton.MouseButton1Click:Connect(function()
    MainFrame.Visible = false
    OpenButton.Visible = true
end)

-- Função para abrir o menu
OpenButton.MouseButton1Click:Connect(function()
    MainFrame.Visible = true
    OpenButton.Visible = false
end)

-- Variáveis para ClickTP
local clickTPActive = false
local teleportTool = Instance.new("Tool")
teleportTool.Name = "ClickTPTool"

-- Função para ativar/desativar ClickTP
ClickTPButton.MouseButton1Click:Connect(function()
    clickTPActive = not clickTPActive
    if clickTPActive then
        ClickTPButton.Text = "ClickTP - ON"
        teleportTool.Parent = game.Players.LocalPlayer.Backpack
    else
        ClickTPButton.Text = "ClickTP - OFF"
        teleportTool.Parent = nil
    end
end)

-- Função de teleporte
teleportTool.Activated:Connect(function()
    local mouse = game.Players.LocalPlayer:GetMouse()
    mouse.Button1Down:Connect(function()
        if clickTPActive then
            game.Players.LocalPlayer.Character:MoveTo(mouse.Hit.p)
        end
    end)
end)

-- Função para duplicar item
DuplicateButton.MouseButton1Click:Connect(function()
    local character = game.Players.LocalPlayer.Character
    local tool = character:FindFirstChildOfClass("Tool")
    if tool then
        local clone = tool:Clone()
        clone.Parent = character
    end
end)
