local Players = game:GetService("Players")
local player = Players.LocalPlayer
local UserInputService = game:GetService("UserInputService")
local TextService = game:GetService("TextService")

-- Create GUI
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "BrainrotLoader"
screenGui.Parent = player:WaitForChild("PlayerGui")

local frame = Instance.new("Frame")
frame.Size = UDim2.new(0, 450, 0, 300)
frame.Position = UDim2.new(0.5, -225, 0.5, -150)
frame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
frame.BorderSizePixel = 0
frame.ClipsDescendants = true
frame.Parent = screenGui

-- Add a cool background effect (subtle gradient)
local gradient = Instance.new("UIGradient")
gradient.Rotation = 90
gradient.Color = ColorSequence.new({
    ColorSequenceKeypoint.new(0, Color3.fromRGB(20, 20, 20)),
    ColorSequenceKeypoint.new(1, Color3.fromRGB(50, 50, 50))
})
gradient.Parent = frame

-- Title bar with drag
local title = Instance.new("TextLabel")
title.Text = "STEAL A BRAINROT LOADER V999 (DRAG ME)"
title.Size = UDim2.new(1, 0, 0, 35)
title.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
title.TextColor3 = Color3.fromRGB(255, 50, 50)
title.Font = Enum.Font.SciFi
title.TextSize = 16
title.Parent = frame

-- Dragging functionality
local dragging = false
local dragInput, dragStart, startPos

title.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 then
        dragging = true
        dragStart = input.Position
        startPos = frame.Position
        input.Changed:Connect(function()
            if input.UserInputState == Enum.UserInputState.End then
                dragging = false
            end
        end)
    end
end)

title.InputChanged:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseMovement then
        dragInput = input
    end
end)

UserInputService.InputChanged:Connect(function(input)
    if input == dragInput and dragging then
        local delta = input.Position - dragStart
        frame.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
    end
end)

-- Status text (replaces loading bar)
local status = Instance.new("TextLabel")
status.Text = "WAITING... 0%"
status.Size = UDim2.new(1, 0, 0, 25)
status.Position = UDim2.new(0, 0, 0.25, 0)
status.BackgroundTransparency = 1
status.TextColor3 = Color3.fromRGB(255, 255, 255)
status.Font = Enum.Font.Code
status.TextSize = 14
status.Parent = frame

-- Main button
local button = Instance.new("TextButton")
button.Text = "JOIN 10M+ MONEY SERVERS"
button.Size = UDim2.new(0.8, 0, 0, 40)
button.Position = UDim2.new(0.1, 0, 0.35, 0)
button.BackgroundColor3 = Color3.fromRGB(200, 0, 0)
button.TextColor3 = Color3.white
button.Font = Enum.Font.GothamBold
button.TextSize = 16
button.Parent = frame

-- Console output box (larger for more logs)
local consoleBox = Instance.new("ScrollingFrame")
consoleBox.Size = UDim2.new(0.9, 0, 0, 120)
consoleBox.Position = UDim2.new(0.05, 0, 0.5, 0)
consoleBox.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
consoleBox.BorderSizePixel = 0
consoleBox.ScrollBarThickness = 5
consoleBox.CanvasSize = UDim2.new(0, 0, 2, 0)
consoleBox.Parent = frame

local consoleText = Instance.new("TextLabel")
consoleText.Size = UDim2.new(1, 0, 2, 0)
consoleText.BackgroundTransparency = 1
consoleText.TextColor3 = Color3.fromRGB(0, 255, 100)
consoleText.Font = Enum.Font.Code
consoleText.TextSize = 12
consoleText.TextXAlignment = Enum.TextXAlignment.Left
consoleText.TextYAlignment = Enum.TextYAlignment.Top
consoleText.Text = "[CONSOLE] Ready to load servers...\n"
consoleText.Parent = consoleBox

-- Copy Job ID Button (for show)
local copyButton = Instance.new("TextButton")
copyButton.Text = "COPY JOB ID"
copyButton.Size = UDim2.new(0.4, 0, 0, 30)
copyButton.Position = UDim2.new(0.3, 0, 0.9, 0)
copyButton.BackgroundColor3 = Color3.fromRGB(0, 100, 255)
copyButton.TextColor3 = Color3.white
copyButton.Font = Enum.Font.GothamBold
copyButton.TextSize = 14
copyButton.Visible = false
copyButton.Parent = frame

-- Close button
local close = Instance.new("TextButton")
close.Text = "X"
close.Size = UDim2.new(0, 25, 0, 25)
close.Position = UDim2.new(1, -25, 0, 0)
close.BackgroundColor3 = Color3.fromRGB(255, 50, 50)
close.TextColor3 = Color3.white
close.Font = Enum.Font.GothamBold
close.Parent = frame

-- Function to update console and status
local function updateConsole(message)
    consoleText.Text = consoleText.Text .. message .. "\n"
    consoleBox.CanvasPosition = Vector2.new(0, consoleText.TextBounds.Y)
    print(message)
end

-- Function to simulate copying to clipboard (fake)
local function fakeCopyToClipboard(text)
    updateConsole("[SYSTEM] Attempting to copy: " .. text)
    updateConsole("[SYSTEM] Setting clipboard data...")
    updateConsole("[SYSTEM] ✓ Successfully copied to clipboard!")
    updateConsole("[SYSTEM] You can now paste (Ctrl+V) in Roblox Studio or game chat")
end

-- Main function
button.MouseButton1Click:Connect(function()
    button.Text = "SCANNING DISCORD..."
    button.Active = false
    copyButton.Visible = false
    consoleText.Text = "[CONSOLE] Starting scan...\n"
    
    -- Simulate connecting to Discord webhook
    updateConsole("[Webhook] Connecting to Discord channel 1401550662335991908...")
    updateConsole("[Webhook] Authenticating with token...")
    updateConsole("[Webhook] ✓ Connection established!")
    
    for i = 1, 100 do
        status.Text = `FETCHING SERVERS... {i}%`
        
        if i % 5 == 0 then
            updateConsole(`[Webhook] Scanning... {i}% complete`)
        end
        
        if i % 10 == 0 then
            local fakeCount = math.random(50, 200) * i
            updateConsole(`[Webhook] Found {fakeCount} servers with 10M+ money`)
        end
        
        task.wait(0.03)
    end

    -- Fake server data
    updateConsole("[Webhook] ✓ Scan complete!")
    updateConsole("[Webhook] ✅ Found 10,000,000+ money servers!")
    updateConsole("")
    updateConsole("[SERVER] JobID: 1234567890 - $10,342,120 - 5 players")
    updateConsole("[SERVER] JobID: 9876543210 - $12,876,543 - 3 players") 
    updateConsole("[SERVER] JobID: 1928374650 - $15,999,999 - 8 players")
    updateConsole("[SERVER] JobID: 5647382910 - $11,234,567 - 2 players")
    updateConsole("[SERVER] JobID: 1092837465 - $13,876,543 - 6 players")
    updateConsole("")
    updateConsole("[SYSTEM] Select a server and click COPY JOB ID")
    
    status.Text = "READY! SELECT A SERVER"
    button.Active = true
    button.Text = "RESCAN SERVERS"
    copyButton.Visible = true
    
    -- Copy button functionality
    copyButton.MouseButton1Click:Connect(function()
        local jobIds = {
            "1234567890",
            "9876543210", 
            "1928374650",
            "5647382910",
            "1092837465"
        }
        local randomJobId = jobIds[math.random(1, #jobIds)]
        fakeCopyToClipboard(randomJobId)
        updateConsole("[SYSTEM] Copied Job ID: " .. randomJobId)
        updateConsole("[SYSTEM] Use game:GetService('TeleportService'):TeleportToPlaceInstance()")
    end)
end)

close.MouseButton1Click:Connect(function()
    screenGui:Destroy()
    print("[Brainrot Loader] GUI closed.")
end)

-- Initial message
updateConsole("[SYSTEM] Brainrot Loader initialized")
updateConsole("[SYSTEM] Click the button to scan for money servers")
