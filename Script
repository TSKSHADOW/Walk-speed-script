-- === Настройки ===
local correctKey = "Don_12E2_KJFT_PIJH_9743"
local speed = 0
local player = game.Players.LocalPlayer
local uis = game:GetService("UserInputService")
local runService = game:GetService("RunService")
local coreGui = game:GetService("CoreGui")

-- Функция закругления
local function round(obj, rad)
    local c = Instance.new("UICorner")
    c.CornerRadius = UDim.new(0, rad)
    c.Parent = obj
end

-- === GUI: Ввод ключа ===
local ScreenGui = Instance.new("ScreenGui", coreGui)

local KeyFrame = Instance.new("Frame", ScreenGui)
KeyFrame.Size = UDim2.new(0, 220, 0, 100)
KeyFrame.Position = UDim2.new(0.5, -110, 0.5, -50)
KeyFrame.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
KeyFrame.Active = true
KeyFrame.Draggable = true
round(KeyFrame, 10)

local KeyTitle = Instance.new("TextLabel", KeyFrame)
KeyTitle.Size = UDim2.new(1, 0, 0, 30)
KeyTitle.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
KeyTitle.Text = "Введите ключ"
KeyTitle.TextColor3 = Color3.fromRGB(255, 255, 255)
KeyTitle.Font = Enum.Font.SourceSansBold
KeyTitle.TextSize = 18
round(KeyTitle, 10)

local KeyBox = Instance.new("TextBox", KeyFrame)
KeyBox.Size = UDim2.new(1, -20, 0, 30)
KeyBox.Position = UDim2.new(0, 10, 0, 40)
KeyBox.PlaceholderText = "Ваш ключ"
KeyBox.Text = ""
KeyBox.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
KeyBox.TextColor3 = Color3.fromRGB(255, 255, 255)
KeyBox.Font = Enum.Font.SourceSans
KeyBox.TextSize = 16
round(KeyBox, 6)

-- === GUI: Ввод скорости ===
local SpeedFrame = Instance.new("Frame", ScreenGui)
SpeedFrame.Size = UDim2.new(0, 200, 0, 120)
SpeedFrame.Position = UDim2.new(0.5, -100, 0.5, -60)
SpeedFrame.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
SpeedFrame.Active = true
SpeedFrame.Draggable = true
SpeedFrame.Visible = false
round(SpeedFrame, 10)

local Title = Instance.new("TextLabel", SpeedFrame)
Title.Size = UDim2.new(1, 0, 0, 30)
Title.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
Title.Text = "Speed Teleport"
Title.TextColor3 = Color3.fromRGB(255, 255, 255)
Title.Font = Enum.Font.SourceSansBold
Title.TextSize = 18
round(Title, 10)

local TextBox = Instance.new("TextBox", SpeedFrame)
TextBox.Size = UDim2.new(1, -20, 0, 30)
TextBox.Position = UDim2.new(0, 10, 0, 40)
TextBox.PlaceholderText = "Введите скорость"
TextBox.Text = ""
TextBox.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
TextBox.TextColor3 = Color3.fromRGB(255, 255, 255)
TextBox.Font = Enum.Font.SourceSans
TextBox.TextSize = 16
round(TextBox, 6)

-- === Бейдж ===
local Badge = Instance.new("Frame", ScreenGui)
Badge.Size = UDim2.new(0, 300, 0, 70)
Badge.Position = UDim2.new(1, 0, 0, 100)
Badge.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
Badge.Visible = false
round(Badge, 10)

local BadgeIcon = Instance.new("ImageLabel", Badge)
BadgeIcon.Size = UDim2.new(0, 60, 0, 60)
BadgeIcon.Position = UDim2.new(0, 5, 0, 5)
BadgeIcon.BackgroundTransparency = 1
BadgeIcon.Image = "rbxassetid://6023426915"

local BadgeText = Instance.new("TextLabel", Badge)
BadgeText.Size = UDim2.new(1, -70, 1, 0)
BadgeText.Position = UDim2.new(0, 70, 0, 0)
BadgeText.Text = "Подпишись на feitan5123"
BadgeText.TextColor3 = Color3.fromRGB(255, 255, 255)
BadgeText.Font = Enum.Font.SourceSansBold
BadgeText.TextSize = 18
BadgeText.BackgroundTransparency = 1
BadgeText.TextXAlignment = Enum.TextXAlignment.Left

-- Показ бейджа
local function showBadge()
    Badge.Visible = true
    Badge.Position = UDim2.new(1, 0, 0, 100)
    Badge:TweenPosition(UDim2.new(1, -310, 0, 100), "Out", "Quad", 0.5, true)
    task.delay(3, function()
        Badge:TweenPosition(UDim2.new(1, 0, 0, 100), "In", "Quad", 0.5, true)
        task.delay(0.5, function() Badge.Visible = false end)
    end)
end

-- Проверка ключа
KeyBox.FocusLost:Connect(function(enterPressed)
    if enterPressed then
        if KeyBox.Text == correctKey then
            KeyFrame.Visible = false
            SpeedFrame.Visible = true
        else
            KeyFrame.Visible = false
            ScreenGui:Destroy()
        end
    end
end)

-- Ввод скорости
TextBox.FocusLost:Connect(function(enterPressed)
    if enterPressed then
        local val = tonumber(TextBox.Text)
        if val then
            speed = val
            showBadge()
        end
    end
end)

-- Движение
local moving = {W=false, A=false, S=false, D=false}
local rootPart

uis.InputBegan:Connect(function(input, gpe)
    if not gpe then
        if input.KeyCode == Enum.KeyCode.W then moving.W = true end
        if input.KeyCode == Enum.KeyCode.A then moving.A = true end
        if input.KeyCode == Enum.KeyCode.S then moving.S = true end
        if input.KeyCode == Enum.KeyCode.D then moving.D = true end
    end
end)

uis.InputEnded:Connect(function(input, gpe)
    if not gpe then
        if input.KeyCode == Enum.KeyCode.W then moving.W = false end
        if input.KeyCode == Enum.KeyCode.A then moving.A = false end
        if input.KeyCode == Enum.KeyCode.S then moving.S = false end
        if input.KeyCode == Enum.KeyCode.D then moving.D = false end
    end
end)

-- Обновление rootPart после смерти
player.CharacterAdded:Connect(function(char)
    repeat task.wait() until char:FindFirstChild("HumanoidRootPart")
    rootPart = char.HumanoidRootPart
end)

-- Инициализация rootPart при первом запуске
if player.Character then
    rootPart = player.Character:FindFirstChild("HumanoidRootPart")
else
    player.CharacterAdded:Wait()
    rootPart = player.Character:FindFirstChild("HumanoidRootPart")
end

-- Основной цикл движения
runService.RenderStepped:Connect(function()
    if speed > 0 and rootPart then
        local moveVector = Vector3.new()

        if moving.W then moveVector = moveVector + (rootPart.CFrame.LookVector * speed) end
        if moving.S then moveVector = moveVector - (rootPart.CFrame.LookVector * speed) end
        if moving.A then moveVector = moveVector - (rootPart.CFrame.RightVector * speed) end
        if moving.D then moveVector = moveVector + (rootPart.CFrame.RightVector * speed) end

        if moveVector.Magnitude > 0 then
            rootPart.CFrame = CFrame.new(rootPart.Position + moveVector)
        end
    end
end)
