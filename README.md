local Players = game:GetService("Players")

-- Function to highlight players
local function highlightPlayers()
    for _, player in pairs(Players:GetPlayers()) do
        -- Skip the local player
        if player ~= Players.LocalPlayer then
            -- Check if the player has a character
            local character = player.Character
            if character then
                -- Create a BillboardGui for the name
                local highlightGui = Instance.new("BillboardGui")
                highlightGui.Name = "HighlightGui"
                highlightGui.Adornee = character:FindFirstChild("HumanoidRootPart")
                highlightGui.Size = UDim2.new(0, 200, 0, 50)
                highlightGui.StudsOffset = Vector3.new(0, 3, 0)
                highlightGui.AlwaysOnTop = true
                highlightGui.Parent = character

                -- Create a TextLabel for the name
                local nameLabel = Instance.new("TextLabel")
                nameLabel.Text = player.Name
                nameLabel.Size = UDim2.new(1, 0, 1, 0)
                nameLabel.BackgroundTransparency = 1
                nameLabel.TextColor3 = Color3.new(1, 1, 1) -- White color
                nameLabel.TextStrokeTransparency = 0 -- Outline for better visibility
                nameLabel.TextScaled = true
                nameLabel.Font = Enum.Font.SourceSansBold
                nameLabel.Parent = highlightGui

                -- Highlight the player with a SelectionBox
                local highlightBox = Instance.new("SelectionBox")
                highlightBox.Adornee = character
                highlightBox.Color3 = Color3.new(1, 0, 0) -- Red color
                highlightBox.LineThickness = 0.05
                highlightBox.Parent = character
            end
        end
    end
end

-- Call the function to highlight players
highlightPlayers()

-- Listen for new players joining
Players.PlayerAdded:Connect(function(player)
    player.CharacterAdded:Connect(function()
        highlightPlayers()
    end)
end)
