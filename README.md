-- ESP Script (LocalScript)

-- Settings
local highlightColor = Color3.fromRGB(255, 0, 0)  -- Red
local nameSize = 14  -- Size of the name text
local nameOffset = Vector3.new(0, 3, 0)  -- Offset from the player's head to show the name

-- Create a function to create ESP for a player
local function createESP(player)
    -- Create a BillboardGui to display the player's name
    local billboardGui = Instance.new("BillboardGui")
    billboardGui.Adornee = player.Character:WaitForChild("Head")
    billboardGui.Size = UDim2.new(0, 100, 0, 50)  -- Size of the name label
    billboardGui.StudsOffset = nameOffset
    billboardGui.Parent = player.Character.Head
    
    -- Create the TextLabel to show the player's name
    local nameLabel = Instance.new("TextLabel")
    nameLabel.Text = player.Name
    nameLabel.Size = UDim2.new(1, 0, 1, 0)
    nameLabel.TextColor3 = Color3.fromRGB(255, 255, 255)  -- White text color
    nameLabel.BackgroundTransparency = 1
    nameLabel.TextSize = nameSize
    nameLabel.TextStrokeTransparency = 0.5
    nameLabel.Parent = billboardGui
    
    -- Highlight the player's character
    local highlight = Instance.new("Highlight")
    highlight.Parent = player.Character
    highlight.FillColor = highlightColor  -- Set the fill color to red
    highlight.OutlineColor = highlightColor  -- Set the outline color to red
    highlight.FillTransparency = 0.5  -- Set the transparency of the fill color
    highlight.OutlineTransparency = 0.2  -- Set the transparency of the outline color
end

-- Loop through all players and create ESP for each one
game.Players.PlayerAdded:Connect(function(player)
    player.CharacterAdded:Connect(function(character)
        -- Make sure the player has a head and wait until the character is fully loaded
        local head = character:WaitForChild("Head")
        
        -- Create ESP for the player
        createESP(player)
    end)
end)

-- Create ESP for players who are already in the game (in case the script runs after they joined)
for _, player in ipairs(game.Players:GetPlayers()) do
    if player.Character then
        createESP(player)
    end
end
