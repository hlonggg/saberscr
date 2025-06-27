-- Saber Simulator Auto Script (Updated June 2025)
local Players = game:GetService("Players")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local LocalPlayer = Players.LocalPlayer
local Workspace = game:GetService("Workspace")

-- Hàm Auto Swing
local function AutoSwing()
    while true do
        if not getgenv().AutoSwing then break end
        ReplicatedStorage.Remotes.SwingSaber:FireServer()
        wait(0.1)
    end
end

-- Hàm Auto Sell với tọa độ cố định
local function AutoSell()
    while true do
        if not getgenv().AutoSell then break end
        local sellAreaPosition = Vector3.new(-150, 4, 250) -- THAY BẰNG TỌA ĐỘ THỰC TẾ CỦA SELL AREA
        if LocalPlayer.Character and LocalPlayer.Character.HumanoidRootPart then
            LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(sellAreaPosition)
            ReplicatedStorage.Remotes.SellStrength:FireServer()
        end
        wait(1.5)
    end
end

-- Hàm Auto Buy Saber
local function AutoBuySaber()
    while true do
        if not getgenv().AutoBuySaber then break end
        for _, saber in pairs(ReplicatedStorage.Sabers:GetChildren()) do
            ReplicatedStorage.Remotes.Swords:FireServer(saber.Name)
        end
        wait(2)
    end
end

-- Hàm Auto Buy DNA
local function AutoBuyDNA()
    while true do
        if not getgenv().AutoBuyDNA then break end
        ReplicatedStorage.Remotes.DNAs:FireServer()
        wait(2)
    end
end

-- Hàm Auto Buy Rank (Class)
local function AutoBuyRank()
    while true do
        if not getgenv().AutoBuyRank then break end
        for _, class in pairs(ReplicatedStorage.Classes:GetChildren()) do
            ReplicatedStorage.Remotes.Classes:FireServer(class.Name)
        end
        wait(2)
    end
end

-- Hàm Auto Farm Boss
local function AutoFarmBoss()
    while true do
        if not getgenv().AutoFarmBoss then break end
        for _, boss in pairs(Workspace.Bosses:GetChildren()) do
            if boss:IsA("Model") and boss:FindFirstChild("Humanoid") and boss.Humanoid.Health > 0 then
                LocalPlayer.Character.HumanoidRootPart.CFrame = boss.HumanoidRootPart.CFrame * CFrame.new(0, 0, -5)
                ReplicatedStorage.Remotes.AttackBoss:FireServer(boss.Name)
            end
        end
        wait(0.5)
    end
end

-- Hàm Auto Hatch Egg (trứng thường)
local function AutoHatchEgg()
    while true do
        if not getgenv().AutoHatchEgg then break end
        local eggName = "1M Egg" -- THAY BẰNG TÊN TRỨNG THƯỜNG (kiểm tra bằng Infinite Yield)
        ReplicatedStorage.Remotes.EggHatchResult:FireServer(eggName)
        wait(1)
    end
end

-- Hàm Auto Hatch Summer Egg (trứng sự kiện)
local function AutoHatchSummerEgg()
    while true do
        if not getgenv().AutoHatchSummerEgg then break end
        local eggName = "SummerEgg" -- THAY BẰNG TÊN TRỨNG SỰ KIỆN (kiểm tra bằng Infinite Yield)
        ReplicatedStorage.Remotes.EggH:FireServer(eggName)
        wait(1)
    end
end

-- Hàm Auto Collect Beach Balls (teleport trực tiếp đến Beach Balls, tốc độ 0.5s)
local function AutoCollectBeachBalls()
    while true do
        if not getgenv().AutoCollectBeachBalls then break end
        if LocalPlayer.Character and LocalPlayer.Character.HumanoidRootPart then
            -- Giả định nhân vật đã ở đảo Summer Event (teleport thủ công qua cổng trước khi bật)
            -- Teleport đến Beach Balls
            for _, ball in pairs(Workspace.EventCurrency:GetChildren()) do
                if ball.Name == "BeachBall" and ball:IsA("BasePart") and ball.Parent then
                    LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(ball.Position)
                    wait(0.5) -- Tốc độ 0.5 giây
                end
            end
            -- Tấn công boss sự kiện để farm thêm Beach Balls
            for _, boss in pairs(Workspace.EventBosses:GetChildren()) do
                if boss:IsA("Model") and boss:FindFirstChild("Humanoid") and boss.Humanoid.Health > 0 then
                    LocalPlayer.Character.HumanoidRootPart.CFrame = boss.HumanoidRootPart.CFrame * CFrame.new(0, 0, -5)
                    ReplicatedStorage.Remotes.AttackBoss:FireServer(boss.Name)
                    wait(0.5)
                end
            end
        end
        wait(0.5)
    end
end

-- Hàm Anti-AFK
local function AntiAFK()
    local VirtualUser = game:GetService("VirtualUser")
    LocalPlayer.Idled:Connect(function()
        VirtualUser:CaptureController()
        VirtualUser:ClickButton2(Vector2.new())
        wait(1)
    end)
end

-- Giao diện GUI (Kavo UI Library)
local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/xHeptc/Kavo-UI-Library/main/source.lua"))()
local Window = Library.CreateLib("Saber Simulator Auto Script - Summer Event 2025", "Ocean")
local Tab = Window:NewTab("Main")
local Section = Tab:NewSection("Auto Features")

-- Toggle cho Auto Swing
Section:NewToggle("Auto Swing", "Tự động vung kiếm", function(state)
    getgenv().AutoSwing = state
    if state then spawn(AutoSwing) end
end)

-- Toggle cho Auto Sell
Section:NewToggle("Auto Sell", "Tự động bán Strength", function(state)
    getgenv().AutoSell = state
    if state then spawn(AutoSell) end
end)

-- Toggle cho Auto Buy Saber
Section:NewToggle("Auto Buy Saber", "Tự động mua kiếm", function(state)
    getgenv().AutoBuySaber = state
    if state then spawn(AutoBuySaber) end
end)

-- Toggle cho Auto Buy DNA
Section:NewToggle("Auto Buy DNA", "Tự động mua DNA", function(state)
    getgenv().AutoBuyDNA = state
    if state then spawn(AutoBuyDNA) end
end)

-- Toggle cho Auto Buy Rank
Section:NewToggle("Auto Buy Rank", "Tự động mua lớp", function(state)
    getgenv().AutoBuyRank = state
    if state then spawn(AutoBuyRank) end
end)

-- Toggle cho Auto Farm Boss
Section:NewToggle("Auto Farm Boss", "Tự động farm boss", function(state)
    getgenv().AutoFarmBoss = state
    if state then spawn(AutoFarmBoss) end
end)

-- Toggle cho Auto Hatch Egg (trứng thường)
Section:NewToggle("Auto Hatch Egg", "Tự động mở trứng thường", function(state)
    getgenv().AutoHatchEgg = state
    if state then spawn(AutoHatchEgg) end
end)

-- Toggle cho Auto Hatch Summer Egg (trứng sự kiện)
Section:NewToggle("Auto Hatch Summer Egg", "Tự động mở Summer Egg", function(state)
    getgenv().AutoHatchSummerEgg = state
    if state then spawn(AutoHatchSummerEgg) end
end)

-- Toggle cho Auto Collect Beach Balls (EVENT)
Section:NewToggle("EVENT - Auto Collect Beach Balls", "Tự động thu thập Beach Balls", function(state)
    getgenv().AutoCollectBeachBalls = state
    if state then
        print("Vui lòng teleport thủ công đến đảo Summer Event trước khi bật toggle!")
        spawn(AutoCollectBeachBalls)
    end
end)

-- Toggle cho Anti-AFK
Section:NewToggle("Anti-AFK", "Ngăn kick khi treo máy", function(state)
    if state then spawn(AntiAFK) end
end)

print("Saber Simulator Auto Script Loaded! -Summer Event 2025")
