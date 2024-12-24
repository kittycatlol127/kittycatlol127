local Players = game:GetService("Players")

-- Function to reset a player repeatedly
local function resetPlayer(player)
    while true do
        -- Check if the player has a character
        if player.Character then
            -- Play a sound to everyone when the player resets
            local sound = Instance.new("Sound")
            sound.SoundId = "rbxassetid://12222242" -- Replace with a sound ID of your choice
            sound.Volume = 5
            sound.PlayOnRemove = true
            sound.Parent = workspace
            sound:Destroy()

            -- Reset the player's character
            player:LoadCharacter()
        end
        wait(0.001) -- Wait 1 millisecond
    end
end

-- Connect the reset function to all players
Players.PlayerAdded:Connect(function(player)
    -- Start resetting the player when they join
    spawn(function()
        resetPlayer(player)
    end)
end)
