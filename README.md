local OrionLib = loadstring(game:HttpGet(('https://pastebin.com/raw/cKSZsPeB')))()
local Window = OrionLib:MakeWindow({Name = "SH HUB", HidePremium = false, SaveConfig = true, ConfigFolder = "OrionTest"})

--[[
Name = <string> - The name of the UI.
HidePremium = <bool> - Whether or not the user details shows Premium status or not.
SaveConfig = <bool> - Toggles the config saving in the UI.
ConfigFolder = <string> - The name of the folder where the configs are saved.
IntroEnabled = <bool> - Whether or not to show the intro animation.
IntroText = <string> - Text to show in the intro animation.
IntroIcon = <string> - URL to the image you want to use in the intro animation.
Icon = <string> - URL to the image you want displayed on the window.
CloseCallback = <function> - Function to execute when the window is closed.
]]


local Tab = Window:MakeTab({
	Name = "main",
	Icon = "rbxassetid://4483345998",
	PremiumOnly = false
})
--[[
Name = <string> - The name of the tab.
Icon = <string> - The icon of the tab.
PremiumOnly = <bool> - Makes the tab accessible to Sirus Premium users only.
]]

Tab:AddParagraph("Ola seja bem vindo ao SH HUB")
Tab:AddParagraph("Este hub foi feito por sh")
Tab:AddParagraph("Dono do hub, sh")
Tab:AddParagraph("para a boombox fucionar pegue o taser azul no inventário")
Tab:AddParagraph("IDS DE ADUDIOS:7337298420 9114397912 2738830850")
Tab:AddParagraph("obrigado por usar o Hub!")
local Tab = Window:MakeTab({
	Name = "audio FE",
	Icon = "rbxassetid://4483345998",
	PremiumOnly = false
})Tab:AddButton({
	Name = "BOOMBOX",
	Callback = function()
	-- Criando a GUI principal
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")
ScreenGui.Enabled = false -- Inicialmente o Frame estarÃƒÂ¡ invisÃƒÂ­vel

-- Criando o frame
local Frame = Instance.new("Frame")
Frame.Parent = ScreenGui
Frame.Size = UDim2.new(0, 400, 0, 200)
Frame.Position = UDim2.new(0.5, -200, 0.5, -100)
Frame.AnchorPoint = Vector2.new(0.5, 0.5)
Frame.BackgroundColor3 = Color3.new(0, 0, 0)
Frame.BackgroundTransparency = 0.3
Frame.BorderSizePixel = 0

-- Adicionando cantos arredondados ao Frame
local UICornerFrame = Instance.new("UICorner")
UICornerFrame.Parent = Frame
UICornerFrame.CornerRadius = UDim.new(0, 15)

-- Criando o texto explicativo
local Label = Instance.new("TextLabel")
Label.Parent = Frame
Label.Size = UDim2.new(1, 0, 0.4, 0)
Label.Position = UDim2.new(0, 0, 0, 0)
Label.Text = "Put in the ID of a sound to play"
Label.TextScaled = true
Label.TextColor3 = Color3.new(1, 1, 1)
Label.BackgroundTransparency = 1
Label.Font = Enum.Font.SciFi

-- Criando a TextBox
local TextBox = Instance.new("TextBox")
TextBox.Parent = Frame
TextBox.Size = UDim2.new(0.8, 0, 0.2, 0)
TextBox.Position = UDim2.new(0.1, 0, 0.5, 0)
TextBox.PlaceholderText = "Enter ID"
TextBox.Text = ""
TextBox.TextScaled = true
TextBox.TextColor3 = Color3.new(1, 1, 1)
TextBox.BackgroundColor3 = Color3.new(0, 0, 0)
TextBox.Font = Enum.Font.SciFi
TextBox.BorderSizePixel = 0

-- Adicionando cantos arredondados Ãƒ  TextBox
local UICornerTextBox = Instance.new("UICorner")
UICornerTextBox.Parent = TextBox
UICornerTextBox.CornerRadius = UDim.new(0, 8)

-- Criando o botÃƒÂ£o
local Button = Instance.new("TextButton")
Button.Parent = Frame
Button.Size = UDim2.new(0.4, 0, 0.2, 0)
Button.Position = UDim2.new(0.3, 0, 0.75, 0)
Button.Text = "Play"
Button.TextScaled = true
Button.TextColor3 = Color3.new(1, 1, 1)
Button.BackgroundColor3 = Color3.new(0, 0, 0)
Button.Font = Enum.Font.SciFi
Button.BorderSizePixel = 0

-- Adicionando cantos arredondados ao botÃƒÂ£o
local UICornerButton = Instance.new("UICorner")
UICornerButton.Parent = Button
UICornerButton.CornerRadius = UDim.new(0, 8)

-- VariÃƒÂ¡vel para armazenar o som em reproduÃƒÂ§ÃƒÂ£o
local currentSound

-- FunÃƒÂ§ÃƒÂ£o para tocar o som localmente
local function playSoundLocally(audioID)
    local character = game.Players.LocalPlayer.Character
    if character and character:FindFirstChild("Head") then
        -- Verifica se jÃƒÂ¡ hÃƒÂ¡ um som sendo tocado e o interrompe
        if currentSound then
            currentSound:Stop()
            currentSound:Destroy()
            currentSound = nil
        end

        -- Cria e toca um novo som
        currentSound = Instance.new("Sound")
        currentSound.Parent = character.Head
        currentSound.SoundId = "rbxassetid://" .. audioID
        currentSound.Volume = 1
        currentSound:Play()

        -- Parar o som apÃƒÂ³s 3 segundos
        task.delay(3, function()
            if currentSound then
                currentSound:Stop()
                currentSound:Destroy()
                currentSound = nil
            end
        end)

        currentSound.Ended:Connect(function()
            if currentSound then
                currentSound:Destroy()
                currentSound = nil
            end
        end)
    else
        warn("NÃƒÂ£o foi possÃƒÂ­vel encontrar a cabeÃƒÂ§a do personagem para tocar o som!")
    end
end

-- FunÃƒÂ§ÃƒÂ£o para enviar o ÃƒÂ¡udio com o ID
Button.MouseButton1Click:Connect(function()
    local audioID = tonumber(TextBox.Text)
    if audioID then
        -- Envia o som para o servidor
        local args = {
            [1] = game:GetService("Players").LocalPlayer.Character.Taser.Handle,
            [2] = audioID,
            [3] = 0.95
        }
        game:GetService("ReplicatedStorage").RE:FindFirstChild("1Gu1nSound1s"):FireServer(unpack(args))

        -- Toca o som localmente
        playSoundLocally(audioID)
    else
        warn("Por favor, insira um ID vÃƒÂ¡lido!")
    end
end)

-- FunÃƒÂ§ÃƒÂ£o para verificar o item "Taser" e controlar o Frame
local function checkForTaser()
    local taserDetected = false

    while true do
        local character = game.Players.LocalPlayer.Character
        local taser = character and character:FindFirstChild("Taser")

        if taser then
            if not taserDetected then
                taserDetected = true
                ScreenGui.Enabled = true

                -- Modificar a "GripPos" do "Taser"
                taser.GripPos = Vector3.new(0, 0, -2)

                -- Executa o cÃƒÂ³digo de "wear" ao equipar o Taser
                local args = {
                    [1] = "wear",
                    [2] = 18756289999
                }
                game:GetService("ReplicatedStorage").RE:FindFirstChild("1Updat1eAvata1r"):FireServer(unpack(args))
            end
        elseif taserDetected then
            taserDetected = false
            ScreenGui.Enabled = false

            -- Executa o cÃƒÂ³digo de "wear" novamente quando o Taser for desequipado
            local args = {
                [1] = "wear",
                [2] = 18756289999
            }
            game:GetService("ReplicatedStorage").RE:FindFirstChild("1Updat1eAvata1r"):FireServer(unpack(args))

            -- Interrompe o som se o Taser for retirado
            if currentSound then
                currentSound:Stop()
                currentSound:Destroy()
                currentSound = nil
            end
        end

        wait(0.1) -- Verifica a cada 0.1 segundos
    end
end

-- Inicia a verificaÃƒÂ§ÃƒÂ£o do item em paralelo
spawn(checkForTaser)

-- Ativando a GUI automaticamente
ScreenGui.Enabled = true
      		print("button pressed")
      end    
})

local Tab = Window:MakeTab({
	Name = "fling",
	Icon = "rbxassetid://4483345998",
	PremiumOnly = false
})

--[[
Name = <string> - The name of the tab.
Icon = <string> - The icon of the tab.
PremiumOnly = <bool> - Makes the tab accessible to Sirus Premium users only.
]]

local function getPlayerNames()
    local players = game:GetService("Players"):GetPlayers()
    local playerNames = {}
    for _, player in ipairs(players) do
        table.insert(playerNames, player.Name)
    end
    return playerNames
end

local teleportLoop

Tab:AddDropdown({
    Name = "lista de jogadores",
    Default = "1",
    Options = getPlayerNames(),
    Callback = function(Value)
        if teleportLoop then
            teleportLoop:Disconnect()
        end
        teleportLoop = game:GetService("RunService").Stepped:Connect(function()
            local targetPlayer = game:GetService("Players"):FindFirstChild(Value)
            if targetPlayer and targetPlayer.Character and targetPlayer.Character:FindFirstChild("HumanoidRootPart") then
                local playerCharacter = game.Players.LocalPlayer.Character
                if playerCharacter and playerCharacter:FindFirstChild("HumanoidRootPart") then
                    playerCharacter.HumanoidRootPart.CFrame = targetPlayer.Character.HumanoidRootPart.CFrame
                end
            end
        end)
    end    
})

game:GetService("Players").PlayerAdded:Connect(function(player)
    Tab:UpdateDropdown({
        Name = "lista de jogadores",
        Options = getPlayerNames(),
        Default = "1"
    })
end)

game:GetService("Players").PlayerRemoving:Connect(function(player)
    Tab:UpdateDropdown({
        Name = "lista de jogadores",
        Options = getPlayerNames(),
        Default = "1"
    })
end)

Tab:AddButton({
	Name = "fling",
	Callback = function()
	loadstring(game:HttpGet("https://rawscripts.net/raw/Universal-Script-Fling-gui-script-13229"))()
      		print("button pressed")
      end    
})

--[[
Name = <string> - The name of the button.
Callback = <function> - The function of the button.
]]

Tab:AddButton({
    Name = "Fling All",
    Callback = function()
  loadstring(game:HttpGet("https://scriptblox.com/raw/Universal-Script-Fe-fling-all-10553"))()
            print("button pressed")
    end    
})

--[[
Name = <string> - The name of the button.
Callback = <function> - The function of the button.
]]

local Tab = Window:MakeTab({
	Name = "itens",
	Icon = "rbxassetid://4483345998",
	PremiumOnly = false
})

--[[
Name = <string> - The name of the tab.
Icon = <string> - The icon of the tab.
PremiumOnly = <bool> - Makes the tab accessible to Sirus Premium users only.
]]

Tab:AddButton({
	Name = "sofá",
	Callback = function()
	local args = {
    [1] = "PickingTools",
    [2] = "Couch"
}
 
game:GetService("ReplicatedStorage").RE:FindFirstChild("1Too1l"):InvokeServer(unpack(args))
      		print("button pressed")
  	end    
})

--[[
Name = <string> - The name of the button.
Callback = <function> - The function of the button.
]]

local Tab = Window:MakeTab({
	Name = "Scripts",
	Icon = "rbxassetid://4483345998",
	PremiumOnly = false
})

--[[
Name = <string> - The name of the tab.
Icon = <string> - The icon of the tab.
PremiumOnly = <bool> - Makes the tab accessible to Sirus Premium users only.
]]

Tab:AddButton({
	Name = "infinite",
	Callback = function()
	loadstring(game:HttpGet('https://raw.githubusercontent.com/EdgeIY/infiniteyield/master/source'))()
      		print("button pressed")
  	end    
})

--[[
Name = <string> - The name of the button.
Callback = <function> - The function of the button.
]]

Tab:AddButton({
	Name = "Ghost hub",
	Callback = function()
	loadstring(game:HttpGet("https://scriptblox.com/raw/Universal-Script-X-Ghost-Hub-X-7595"))()
      		print("button pressed")
  	end    
})
Tab:AddButton({
	Name = "fly v3",
	Callback = function()
	loadstring(game:HttpGet("https://rawscripts.net/raw/Universal-Script-Fly-v3-7412"))()
      		print("button pressed")
  	end    
})

--[[
Name = <string> - The name of the button.
Callback = <function> - The function of the button.
]]

-- Create a tab
local Tab = Window:MakeTab({
    Name = "Casas",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

local a = 0

Tab:AddTextbox({
    Name = "Numero",
    Default = "11",
    TextDisappear = true,
    Callback = function(Value)
        a = tonumber(Value) or 0  -- Converte o valor para nÃºmero ou define como 0 se nÃ£o for um nÃºmero vÃ¡lido
    end      
})

Tab:AddButton({
    Name = "pegar permissao",
    Callback = function()
        local args = {
            "GivePermissionLoopToServer",
            game.Players.LocalPlayer,
            a
        }

        game:GetService("ReplicatedStorage").RE:FindFirstChild("1Playe1rTrigge1rEven1t"):FireServer(unpack(args))
    end    
})
