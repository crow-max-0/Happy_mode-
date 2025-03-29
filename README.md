local ScreenGui = Instance.new("ScreenGui")
local Frame = Instance.new("Frame")
local Title = Instance.new("TextLabel")
local CloseButton = Instance.new("TextButton")

local Options = {
    "HDR GRAPHICS",
    "WALL HACK",
    "MULTI JUMPS",
    "SPEED",
    "FLY HOLD",
    "TELEPORT UP"
}

-- UI 설정
ScreenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")

Frame.Parent = ScreenGui
Frame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
Frame.Size = UDim2.new(0, 200, 0, 250)
Frame.Position = UDim2.new(0.1, 0, 0.1, 0)

Title.Parent = Frame
Title.Text = "GameDVA.com - Menu mod"
Title.Size = UDim2.new(1, 0, 0, 30)
Title.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
Title.TextColor3 = Color3.fromRGB(255, 255, 255)

CloseButton.Parent = Frame
CloseButton.Size = UDim2.new(0, 30, 0, 30)
CloseButton.Position = UDim2.new(1, -30, 0, 0)
CloseButton.Text = "X"
CloseButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
CloseButton.TextColor3 = Color3.fromRGB(255, 255, 255)

CloseButton.MouseButton1Click:Connect(function()
    ScreenGui:Destroy()
end)

-- 기능 구현
local function EnableHDRGraphics()
    game.Lighting.Brightness = 2
    game.Lighting.GlobalShadows = true
    game.Lighting.FogEnd = 100000
    print("HDR Graphics 적용됨!")
end

local function EnableWallHack()
    for _, v in pairs(workspace:GetDescendants()) do
        if v:IsA("BasePart") then
            v.CanCollide = false
        end
    end
    print("Wall Hack 활성화됨!")
end

local function EnableMultiJumps()
    local player = game.Players.LocalPlayer
    local humanoid = player.Character and player.Character:FindFirstChildOfClass("Humanoid")

    if humanoid then
        humanoid:SetStateEnabled(Enum.HumanoidStateType.Jumping, true)
        humanoid.JumpPower = 100  -- 점프력 증가
        print("Multi Jumps 활성화됨!")
    end
end

local function EnableTeleportUp()
    local player = game.Players.LocalPlayer
    local character = player.Character
    if character and character:FindFirstChild("HumanoidRootPart") then
        character.HumanoidRootPart.CFrame = character.HumanoidRootPart.CFrame + Vector3.new(0, 50, 0)
        print("위로 순간이동 완료!")
    end
end

-- 옵션 버튼 생성
for i, option in ipairs(Options) do
    local Button = Instance.new("TextButton")
    Button.Parent = Frame
    Button.Size = UDim2.new(1, -20, 0, 30)
    Button.Position = UDim2.new(0, 10, 0, 30 + (i - 1) * 35)
    Button.Text = option
    Button.BackgroundColor3 = Color3.fromRGB(200, 0, 0)
    Button.TextColor3 = Color3.fromRGB(255, 255, 255)

    Button.MouseButton1Click:Connect(function()
        if option == "HDR GRAPHICS" then
            EnableHDRGraphics()
        elseif option == "WALL HACK" then
            EnableWallHack()
        elseif option == "MULTI JUMPS" then
            EnableMultiJumps()
        elseif option == "SPEED" then
            loadstring(game:HttpGet('https://raw.githubusercontent.com/crow-max-0/Sp/refs/heads/main/README.md'))()
        elseif option == "FLY HOLD" then
            loadstring("\108\111\97\100\115\116\114\105\110\103\40\103\97\109\101\58\72\116\116\112\71\101\116\40\40\39\104\116\116\112\115\58\47\47\103\105\115\116\46\103\105\116\104\117\98\117\115\101\114\99\111\110\116\101\110\116\46\99\111\109\47\109\101\111\122\111\110\101\89\84\47\98\102\48\51\55\100\102\102\57\102\48\97\55\48\48\49\55\51\48\52\100\100\100\54\55\102\100\99\100\51\55\48\47\114\97\119\47\101\49\52\101\55\52\102\52\50\53\98\48\54\48\100\102\53\50\51\51\52\51\99\102\51\48\98\55\56\55\48\55\52\101\98\51\99\53\100\50\47\97\114\99\101\117\115\37\50\53\50\48\120\37\50\53\50\48\102\108\121\37\50\53\50\48\50\37\50\53\50\48\111\98\102\108\117\99\97\116\111\114\39\41\44\116\114\117\101\41\41\40\41\10\10")()
        elseif option == "TELEPORT UP" then
            EnableTeleportUp()
        else
            print(option .. " 버튼 클릭됨!")
        end
    end)
end
