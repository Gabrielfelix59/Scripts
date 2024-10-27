if game.PlaceId == 2753915549 then
    World1 = true
elseif game.PlaceId == 4442272183 then
    World2 = true
elseif game.PlaceId == 7449423635 then
    World3 = true
else
    game:GetService("Players").LocalPlayer:Kick("Do not Support, Please wait...")
end

local isRunning = false

local ScreenGui = Instance.new("ScreenGui")
local Frame = Instance.new("Frame")
local StartButton = Instance.new("TextButton")
local StopButton = Instance.new("TextButton")

Frame.Parent = ScreenGui
Frame.Size = UDim2.new(0, 200, 0, 100)
Frame.Position = UDim2.new(0.5, -100, 0.5, -50)
Frame.BackgroundColor3 = Color3.new(0.2, 0.2, 0.2)
Frame.BorderSizePixel = 0

StartButton.Parent = Frame
StartButton.Size = UDim2.new(1, 0, 0.5, 0)
StartButton.BackgroundColor3 = Color3.new(0, 1, 0)
StartButton.Text = "Iniciar"
StartButton.Font = Enum.Font.SourceSans
StartButton.TextSize = 24
StartButton.TextColor3 = Color3.new(1, 1, 1)

StopButton.Parent = Frame
StopButton.Size = UDim2.new(1, 0, 0.5, 0)
StopButton.Position = UDim2.new(0, 0, 0.5, 0)
StopButton.BackgroundColor3 = Color3.new(1, 0, 0)
StopButton.Text = "Parar"
StopButton.Font = Enum.Font.SourceSans
StopButton.TextSize = 24
StopButton.TextColor3 = Color3.new(1, 1, 1)

function CheckQuest()
    local MyLevel = game:GetService("Players").LocalPlayer.Data.Level.Value
    if World1 then
        if MyLevel <= 9 then
            return "Bandit", "BanditQuest1", CFrame.new(1059.37195, 15.4495068, 1550.4231), CFrame.new(1045.962646484375, 27.00250816345215, 1560.8203125)
        elseif MyLevel <= 14 then
            return "Monkey", "JungleQuest", CFrame.new(-1598.08911, 35.5501175, 153.377838), CFrame.new(-1448.51806640625, 67.85301208496094, 11.46579647064209)
        elseif MyLevel <= 29 then
            return "Gorilla", "JungleQuest", CFrame.new(-1598.08911, 35.5501175, 153.377838), CFrame.new(-1129.8836669921875, 40.46354675292969, -525.4237060546875)
        elseif MyLevel <= 39 then
            return "Pirate", "BuggyQuest1", CFrame.new(-1141.07483, 4.10001802, 3831.5498), CFrame.new(-1103.513427734375, 13.752052307128906, 3896.091064453125)
        elseif MyLevel <= 59 then
            return "Brute", "BuggyQuest1", CFrame.new(-1141.07483, 4.10001802, 3831.5498), CFrame.new(-1140.083740234375, 14.809885025024414, 4322.92138671875)
        elseif MyLevel <= 74 then
            return "Desert Bandit", "DesertQuest", CFrame.new(894.488647, 5.14000702, 4392.43359), CFrame.new(924.7998046875, 6.44867467880249, 4481.5859375)
        elseif MyLevel <= 89 then
            return "Desert Officer", "DesertQuest", CFrame.new(894.488647, 5.14000702, 4392.43359), CFrame.new(1608.2822265625, 8.614224433898926, 4371.00732421875)
        elseif MyLevel <= 99 then
            return "Snow Bandit", "SnowQuest", CFrame.new(1389.74451, 88.1519318, -1298.90796), CFrame.new(1354.347900390625, 87.27277374267578, -1393.946533203125)
        elseif MyLevel <= 119 then
            return "Snowman", "SnowQuest", CFrame.new(1389.74451, 88.1519318, -1298.90796), CFrame.new(1201.6412353515625, 144.57958984375, -1550.0670166015625)
        elseif MyLevel <= 149 then
            return "Chief Petty Officer", "NextQuest", CFrame.new(0, 0, 0), CFrame.new(0, 0, 0)
        end
    end
end

function pegarMissao()
    local Mon, NameQuest, CFrameQuest, CFrameMon = CheckQuest()
    if Mon and NameQuest then
        print("Pegando missão: " .. NameQuest .. " contra " .. Mon)
        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrameQuest
        wait(1)
    end
end

function derrotarNPC()
    local Mon, _, _, CFrameMon = CheckQuest()
    if Mon then
        print("Derrotando " .. Mon)
        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrameMon
        wait(1)
    end
end

function startMission()
    isRunning = true
    while isRunning do
        pegarMissao()
        derrotarNPC()
        wait(2)
    end
end

StartButton.MouseButton1Click:Connect(function()
    if not isRunning then
        startMission()
    end
end)

StopButton.MouseButton1Click:Connect(function()
    isRunning = false
end)

ScreenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")

