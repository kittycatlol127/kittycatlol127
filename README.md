-- LocalScript: StarterPlayerScripts

-- Create the Screen GUI
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "ChatAI"
screenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")

-- Create the Frame for the Chatbox
local chatFrame = Instance.new("Frame", screenGui)
chatFrame.Size = UDim2.new(0.4, 0, 0.3, 0)
chatFrame.Position = UDim2.new(0.3, 0, 0.6, 0)
chatFrame.BackgroundColor3 = Color3.new(0.2, 0.2, 0.2)
chatFrame.BorderSizePixel = 0

-- Create a TextBox for Player Input
local inputBox = Instance.new("TextBox", chatFrame)
inputBox.Size = UDim2.new(0.8, 0, 0.2, 0)
inputBox.Position = UDim2.new(0.1, 0, 0.7, 0)
inputBox.PlaceholderText = "Type your message here..."
inputBox.Text = ""
inputBox.TextScaled = true
inputBox.BackgroundColor3 = Color3.new(0.3, 0.3, 0.3)
inputBox.TextColor3 = Color3.new(1, 1, 1)
inputBox.BorderSizePixel = 0

-- Create a TextLabel for AI Responses
local responseLabel = Instance.new("TextLabel", chatFrame)
responseLabel.Size = UDim2.new(0.8, 0, 0.5, 0)
responseLabel.Position = UDim2.new(0.1, 0, 0.1, 0)
responseLabel.Text = "Hello! How can I help you today?"
responseLabel.TextScaled = true
responseLabel.BackgroundColor3 = Color3.new(0.3, 0.3, 0.3)
responseLabel.TextColor3 = Color3.new(1, 1, 1)
responseLabel.BorderSizePixel = 0

-- Function to Handle AI Responses
local function getResponse(message)
    local lowerMessage = string.lower(message) -- Convert message to lowercase for easier comparison

    if string.find(lowerMessage, "hello") then
        return "Hi there! How are you?"
    elseif string.find(lowerMessage, "how are you") then
        return "I'm just a script, but I'm here to help!"
    elseif string.find(lowerMessage, "help") then
        return "What do you need help with?"
    elseif string.find(lowerMessage, "bye") then
        return "Goodbye! Have a great day!"
    else
        return "I don't understand that. Could you try saying it differently?"
    end
end

-- Event for Detecting Player Input
inputBox.FocusLost:Connect(function(enterPressed)
    if enterPressed and inputBox.Text ~= "" then
        -- Get the AI's response
        local playerMessage = inputBox.Text
        local aiResponse = getResponse(playerMessage)

        -- Display the AI's response
        responseLabel.Text = aiResponse

        -- Clear the input box
        inputBox.Text = ""
    end
end)
