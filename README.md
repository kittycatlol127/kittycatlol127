-- LocalScript: StarterPlayerScripts

local player = game.Players.LocalPlayer
local screenGui = Instance.new("ScreenGui", player.PlayerGui)
screenGui.Name = "NukeButtonGUI"

-- Create the red button
local nukeButton = Instance.new("TextButton", screenGui)
nukeButton.Size = UDim2.new(0.2, 0, 0.1, 0)
nukeButton.Position = UDim2.new(0.4, 0, 0.8, 0)
nukeButton.Text = "NUKE"
nukeButton.TextScaled = true
nukeButton.BackgroundColor3 = Color3.new(1, 0, 0) -- Red
nukeButton.TextColor3 = Color3.new(1, 1, 1) -- White text
nukeButton.BorderSizePixel = 2
nukeButton.BorderColor3 = Color3.new(0.5, 0, 0) -- Darker border

-- Function to fling all players
local function flingEveryone()
    for _, otherPlayer in pairs(game.Players:GetPlayers()) do
        if otherPlayer.Character and otherPlayer.Character:FindFirstChild("HumanoidRootPart") then
            local rootPart = otherPlayer.Character.HumanoidRootPart
            -- Apply a large random force to fling the player
            rootPart.Velocity = Vector3.new(
                math.random(-1000, 1000), -- Random force on X
                math.random(500, 1500),  -- Random upward force
                math.random(-1000, 1000) -- Random force on Z
            )
        end
    end
end

-- Button click event
nukeButton.MouseButton1Click:Connect(function()
    -- Change button appearance on click
    nukeButton.BackgroundColor3 = Color3.new(0.5, 0, 0) -- Darker red
    nukeButton.Size = UDim2.new(0.18, 0, 0.09, 0) -- Slightly smaller
    flingEveryone()

    -- Wait and reset the button appearance
    task.wait(0.2)
    nukeButton.BackgroundColor3 = Color3.new(1, 0, 0) -- Original red
    nukeButton.Size = UDim2.new(0.2, 0, 0.1, 0) -- Original size
end)
