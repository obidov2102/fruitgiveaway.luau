local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer

local gui = Instance.new("ScreenGui", LocalPlayer:WaitForChild("PlayerGui"))
gui.Name = "TradeGUI"

local frame = Instance.new("Frame", gui)
frame.Size = UDim2.new(0, 300, 0, 170)
frame.Position = UDim2.new(0.5, -150, 0.5, -85)
frame.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
frame.BorderSizePixel = 0

local title = Instance.new("TextLabel", frame)
title.Size = UDim2.new(1, 0, 0.25, 0)
title.Text = "🤝 Trade Panel"
title.TextScaled = true
title.TextColor3 = Color3.new(1, 1, 1)
title.BackgroundTransparency = 1

local userBox = Instance.new("TextBox", frame)
userBox.PlaceholderText = "Foydalanuvchi ismi"
userBox.Size = UDim2.new(0.9, 0, 0.25, 0)
userBox.Position = UDim2.new(0.05, 0, 0.3, 0)
userBox.TextScaled = true
userBox.Text = ""

local tpButton = Instance.new("TextButton", frame)
tpButton.Size = UDim2.new(0.42, 0, 0.25, 0)
tpButton.Position = UDim2.new(0.05, 0, 0.6, 0)
tpButton.Text = "📍 TP To User"
tpButton.TextScaled = true
tpButton.BackgroundColor3 = Color3.fromRGB(0, 100, 180)
tpButton.TextColor3 = Color3.new(1,1,1)

local tradeButton = Instance.new("TextButton", frame)
tradeButton.Size = UDim2.new(0.42, 0, 0.25, 0)
tradeButton.Position = UDim2.new(0.53, 0, 0.6, 0)
tradeButton.Text = "🤝 Send Trade"
tradeButton.TextScaled = true
tradeButton.BackgroundColor3 = Color3.fromRGB(0, 150, 0)
tradeButton.TextColor3 = Color3.new(1,1,1)

tpButton.MouseButton1Click:Connect(function()
    local user = userBox.Text
    local target = Players:FindFirstChild(user)
    if target and target.Character and target.Character:FindFirstChild("HumanoidRootPart") then
        LocalPlayer.Character.HumanoidRootPart.CFrame = target.Character.HumanoidRootPart.CFrame + Vector3.new(2,0,0)
    end
end)

tradeButton.MouseButton1Click:Connect(function()
    local user = userBox.Text
    if Players:FindFirstChild(user) then
        title.Text = "✅ Trade boshlangan — o‘yindagi tizim orqali yakunlang!"
    else
        title.Text = "❌ O‘yinchi topilmadi."
    end
end)
https://raw.githubusercontent.com/obidov2102/bloxfruit-gui/main/tradegui.luau
