-- LocalScript (colocar em StarterGui)
-- Cria a GUI arrastável, botão fechar (X) e botão pequeno para reabrir.
-- Envia pedidos ao servidor para "show" / "hide" do Billboard (servidor decide quem pode).

local ReplicatedStorage = game:GetService("ReplicatedStorage")
local UserInputService = game:GetService("UserInputService")
local Players = game:GetService("Players")
local player = Players.LocalPlayer

local remote = ReplicatedStorage:WaitForChild("CoolkidRemote")

local function new(class, props)
    local obj = Instance.new(class)
    if props then
        for k, v in pairs(props) do obj[k] = v end
    end
    return obj
end

local screenGui = new("ScreenGui", player:WaitForChild("PlayerGui"))
screenGui.Name = "CoolkidScreenGui"
screenGui.ResetOnSpawn = false

local frame = new("Frame", screenGui)
frame.Name = "MainFrame"
frame.Size = UDim2.new(0, 320, 0, 160)
frame.Position = UDim2.new(0.5, -160, 0.3, -80)
frame.BackgroundColor3 = Color3.fromRGB(30, 30, 40)
frame.BorderSizePixel = 0
frame.Active = true

local title = new("TextLabel", frame)
title.Size = UDim2.new(1, -10, 0, 30)
title.Position = UDim2.new(0, 5, 0, 5)
title.BackgroundTransparency = 1
title.Text = "CoolKid - Painel"
title.TextColor3 = Color3.new(1,1,1)
title.TextScaled = true
title.Font = Enum.Font.SourceSansBold
title.TextXAlignment = Enum.TextXAlignment.Left

local closeBtn = new("TextButton", frame)
closeBtn.Size = UDim2.new(0, 26, 0, 26)
closeBtn.Position = UDim2.new(1, -30, 0, 4)
closeBtn.Text = "X"
closeBtn.Font = Enum.Font.SourceSansBold
closeBtn.TextSize = 18
closeBtn.BackgroundColor3 = Color3.fromRGB(180, 60, 60)
closeBtn.TextColor3 = Color3.new(1,1,1)
closeBtn.AutoButtonColor = true

local visibleBtn = new("TextButton", frame)
visibleBtn.Name = "ToggleServerVisible"
visibleBtn.Size = UDim2.new(0, 160, 0, 36)
visibleBtn.Position = UDim2.new(0.5, -80, 0, 60)
visibleBtn.Text = "Mostrar para todos (servidor)"
visibleBtn.Font = Enum.Font.SourceSans
visibleBtn.TextSize = 14
visibleBtn.BackgroundColor3 = Color3.fromRGB(75, 135, 255)
visibleBtn.TextColor3 = Color3.new(1,1,1)
visibleBtn.AutoButtonColor = true

local textBox = new("TextBox", frame)
textBox.PlaceholderText = "Texto a mostrar no Billboard"
textBox.Size = UDim2.new(1, -20, 0, 28)
textBox.Position = UDim2.new(0, 10, 0, 104)
textBox.BackgroundColor3 = Color3.fromRGB(45,45,55)
textBox.TextColor3 = Color3.fromRGB(230,230,230)
textBox.Text = ""

local reopenBtn = new("TextButton", screenGui)
reopenBtn.Name = "ReopenBtn"
reopenBtn.Size = UDim2.new(0, 160, 0, 36)
reopenBtn.Position = UDim2.new(0.02, 0, 0.8, 0)
reopenBtn.Text = "Abrir CoolKid"
reopenBtn.Visible = false
reopenBtn.BackgroundColor3 = Color3.fromRGB(60, 
