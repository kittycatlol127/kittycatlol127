-- LocalScript: StarterPlayerScripts

-- Check if the player is on a mobile device
if game:GetService("UserInputService").TouchEnabled then
    local player = game.Players.LocalPlayer
    local character = player.Character or player.CharacterAdded:Wait()
    local humanoid = character:WaitForChild("Humanoid")
    local rootPart = character:WaitForChild("HumanoidRootPart")
    
    -- GUI Setup
    local screenGui = Instance.new("ScreenGui", player.PlayerGui)
    screenGui.Name = "FlightControls"

    -- Speed Adjustment Box
    local speedBox = Instance.new("TextBox", screenGui)
    speedBox.Size = UDim2.new(0.3, 0, 0.1, 0)
    speedBox.Position = UDim2.new(0.35, 0, 0.8, 0)
    speedBox.Text = "50" -- Default speed
    speedBox.TextScaled = true
    speedBox.BackgroundColor3 = Color3.new(0, 0, 0.5)
    speedBox.TextColor3 = Color3.new(1, 1, 1)
    speedBox.PlaceholderText = "Enter Speed"

    -- Fly Button
    local flyButton = Instance.new("TextButton", screenGui)
    flyButton.Size = UDim2.new(0.3, 0, 0.1, 0)
    flyButton.Position = UDim2.new(0.1, 0, 0.9, 0)
    flyButton.Text = "Fly"
    flyButton.TextScaled = true
    flyButton.BackgroundColor3 = Color3.new(0, 0.5, 0)
    flyButton.TextColor3 = Color3.new(1, 1, 1)

    -- Stop Button
    local stopButton = Instance.new("TextButton", screenGui)
    stopButton.Size = UDim2.new(0.3, 0, 0.1, 0)
    stopButton.Position = UDim2.new(0.6, 0, 0.9, 0)
    stopButton.Text = "Stop"
    stopButton.TextScaled = true
    stopButton.BackgroundColor3 = Color3.new(0.5, 0, 0)
    stopButton.TextColor3 = Color3.new(1, 1, 1)

    -- Fly Logic
    local flying = false
    local speed = 50

    local function startFlying()
        flying = true
        while flying do
            task.wait()
            local direction = humanoid.MoveDirection
            rootPart.Velocity = Vector3.new(direction.X * speed, speed, direction.Z * speed)
        end
    end

    local function stopFlying()
        flying = false
        rootPart.Velocity = Vector3.zero
    end

    -- Button Events
    flyButton.MouseButton1Click:Connect(function()
        speed = tonumber(speedBox.Text) or 50
        startFlying()
    end)

    stopButton.MouseButton1Click:Connect(stopFlying)
else
    warn("This script is only for mobile devices.")
end
