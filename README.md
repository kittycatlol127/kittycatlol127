-- LocalScript: StarterPlayerScripts

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

    -- Flying Logic
    local flying = false
    local speed = 50
    local bodyGyro = Instance.new("BodyGyro")
    local bodyVelocity = Instance.new("BodyVelocity")

    bodyGyro.MaxTorque = Vector3.new(1e6, 1e6, 1e6) -- Allow rotation in all axes
    bodyGyro.P = 3e4
    bodyGyro.D = 100

    bodyVelocity.MaxForce = Vector3.new(1e6, 1e6, 1e6) -- Allow movement in all directions
    bodyVelocity.P = 1e4

    local function startFlying()
        flying = true
        bodyGyro.Parent = rootPart
        bodyVelocity.Parent = rootPart

        while flying do
            task.wait()

            -- Get movement direction and rotation
            local moveDirection = humanoid.MoveDirection
            local lookVector = rootPart.CFrame.LookVector

            -- Set velocity based on input direction
            bodyVelocity.Velocity = (lookVector * moveDirection.Magnitude * speed) + Vector3.new(0, moveDirection.Y * speed, 0)

            -- Rotate towards the movement direction
            if moveDirection.Magnitude > 0 then
                bodyGyro.CFrame = CFrame.new(rootPart.Position, rootPart.Position + moveDirection)
            end
        end
    end

    local function stopFlying()
        flying = false
        bodyVelocity:Destroy()
        bodyGyro:Destroy()
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
