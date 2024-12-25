local player = game.Players.LocalPlayer
local mouse = player:GetMouse()
local flying = false
local speed = 50
local flyGui = Instance.new("ScreenGui")
local frame = Instance.new("Frame")
local speedBox = Instance.new("TextBox")

-- Create GUI for speed adjustment
flyGui.Name = "FlyGui"
flyGui.Parent = player:WaitForChild("PlayerGui")

frame.Size = UDim2.new(0, 200, 0, 100)
frame.Position = UDim2.new(0.5, -100, 0.1, 0)
frame.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
frame.Parent = flyGui

speedBox.Size = UDim2.new(0, 150, 0, 50)
speedBox.Position = UDim2.new(0.5, -75, 0.5, -25)
speedBox.Text = tostring(speed)
speedBox.PlaceholderText = "Speed"
speedBox.TextColor3 = Color3.fromRGB(255, 255, 255)
speedBox.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
speedBox.Parent = frame

-- Flying function
local bodyGyro, bodyVelocity

local function startFlying()
    if not flying then
        flying = true
        local character = player.Character or player.CharacterAdded:Wait()
        local rootPart = character:WaitForChild("HumanoidRootPart")

        bodyGyro = Instance.new("BodyGyro")
        bodyGyro.MaxTorque = Vector3.new(400000, 400000, 400000)
        bodyGyro.CFrame = rootPart.CFrame
        bodyGyro.Parent = rootPart

        bodyVelocity = Instance.new("BodyVelocity")
        bodyVelocity.MaxForce = Vector3.new(400000, 400000, 400000)
        bodyVelocity.Velocity = Vector3.zero
        bodyVelocity.Parent = rootPart

        while flying do
            bodyGyro.CFrame = workspace.CurrentCamera.CFrame
            bodyVelocity.Velocity = workspace.CurrentCamera.CFrame.LookVector * speed
            wait()
        end
    end
end

local function stopFlying()
    flying = false
    if bodyGyro then bodyGyro:Destroy() end
    if bodyVelocity then bodyVelocity:Destroy() end
end

-- Toggle flying with button press (mobile-compatible)
local UIS = game:GetService("UserInputService")

UIS.InputBegan:Connect(function(input, processed)
    if processed then return end
    if input.UserInputType == Enum.UserInputType.Touch or input.KeyCode == Enum.KeyCode.Space then
        if flying then
            stopFlying()
        else
            startFlying()
        end
    end
end)

-- Update speed based on the speedBox value
speedBox.FocusLost:Connect(function(enterPressed)
    if enterPressed then
        local newSpeed = tonumber(speedBox.Text)
        if newSpeed and newSpeed > 0 then
            speed = newSpeed
        else
            speedBox.Text = tostring(speed) -- Reset invalid input
        end
    end
end)

-- Stop flying on character respawn
player.CharacterAdded:Connect(function()
    stopFlying()
end)
