local TweenService = game:GetService("TweenService")
local Players = game:GetService("Players")
local UserInputService = game:GetService("UserInputService")

-- Create ScreenGui
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Parent = Players.LocalPlayer:WaitForChild("PlayerGui")

-- Create Loading Screen
local LoadingScreen = Instance.new("Frame")
LoadingScreen.Size = UDim2.new(1, 0, 1, 0)
LoadingScreen.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
LoadingScreen.Parent = ScreenGui

local LoadingText = Instance.new("TextLabel")
LoadingText.Size = UDim2.new(1, 0, 0.1, 0)
LoadingText.Position = UDim2.new(0, 0, 0.45, 0)
LoadingText.BackgroundTransparency = 1
LoadingText.TextColor3 = Color3.fromRGB(255, 255, 255)
LoadingText.Text = "Made by Voorlove Music. Subscribe to my channel!"
LoadingText.Font = Enum.Font.GothamBold
LoadingText.TextSize = 20
LoadingText.Parent = LoadingScreen

-- Tween for loading text
local tweenInfo = TweenInfo.new(1, Enum.EasingStyle.Quad, Enum.EasingDirection.Out)
local tweenIn = TweenService:Create(LoadingText, tweenInfo, {TextTransparency = 0})
local tweenOut = TweenService:Create(LoadingText, tweenInfo, {TextTransparency = 1})

-- Create Frame for the main GUI (smaller size)
local Frame = Instance.new("Frame")
Frame.Size = UDim2.new(0.3, 0, 0.3, 0) -- Adjusted size
Frame.Position = UDim2.new(0.35, 0, 0.35, 0)
Frame.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
Frame.Visible = false  -- Start hidden
Frame.Parent = ScreenGui

-- Create TextBox for amount to steal
local amountTextBox = Instance.new("TextBox")
amountTextBox.Size = UDim2.new(0.8, 0, 0.2, 0)
amountTextBox.Position = UDim2.new(0.1, 0, 0.1, 0)
amountTextBox.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
amountTextBox.PlaceholderText = "Amount to steal"
amountTextBox.Font = Enum.Font.GothamBold
amountTextBox.TextSize = 16
amountTextBox.TextColor3 = Color3.fromRGB(0, 0, 0)
amountTextBox.Parent = Frame

-- Create Button to steal time
local stealButton = Instance.new("TextButton")
stealButton.Size = UDim2.new(0.8, 0, 0.2, 0)
stealButton.Position = UDim2.new(0.1, 0, 0.35, 0)
stealButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
stealButton.Text = "Steal from Admin"
stealButton.Font = Enum.Font.GothamBold
stealButton.TextSize = 16
stealButton.TextColor3 = Color3.fromRGB(255, 255, 255)
stealButton.Parent = Frame

-- Create Button to add Infinity symbol
local addInfButton = Instance.new("TextButton")
addInfButton.Size = UDim2.new(0.8, 0, 0.2, 0)
addInfButton.Position = UDim2.new(0.1, 0, 0.65, 0) -- Position below the steal button
addInfButton.BackgroundColor3 = Color3.fromRGB(0, 255, 0) -- Green color
addInfButton.Text = "Add Infinity"
addInfButton.Font = Enum.Font.GothamBold
addInfButton.TextSize = 16
addInfButton.TextColor3 = Color3.fromRGB(255, 255, 255)
addInfButton.Parent = Frame

-- Create Close Button
local closeButton = Instance.new("TextButton")
closeButton.Size = UDim2.new(0.1, 0, 0.1, 0)
closeButton.Position = UDim2.new(0.9, 0, 0, 0)
closeButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
closeButton.Text = "X"
closeButton.Font = Enum.Font.GothamBold
closeButton.TextSize = 16
closeButton.TextColor3 = Color3.fromRGB(255, 255, 255)
closeButton.Parent = Frame

-- Create Static Rainbow TextLabel for V1
local rainbowLabel = Instance.new("TextLabel")
rainbowLabel.Size = UDim2.new(0.8, 0, 0.1, 0)
rainbowLabel.Position = UDim2.new(0.1, 0, 0.85, 0) -- Position under the Add Infinity button
rainbowLabel.BackgroundTransparency = 1
rainbowLabel.TextColor3 = Color3.fromRGB(255, 0, 0) -- Red color for "V1"
rainbowLabel.Text = "V1"
rainbowLabel.Font = Enum.Font.GothamBold
rainbowLabel.TextSize = 30
rainbowLabel.Parent = Frame

-- Create TextLabel to display stolen amount
local stolenAmountLabel = Instance.new("TextLabel")
stolenAmountLabel.Size = UDim2.new(0.8, 0, 0.1, 0)
stolenAmountLabel.Position = UDim2.new(0.1, 0, 0.5, 0)
stolenAmountLabel.BackgroundTransparency = 1
stolenAmountLabel.TextColor3 = Color3.fromRGB(255, 255, 0) -- Yellow color for displayed amount
stolenAmountLabel.Text = "Stolen Amount: 0"
stolenAmountLabel.Font = Enum.Font.GothamBold
stolenAmountLabel.TextSize = 20
stolenAmountLabel.Parent = Frame
