local Players = game:GetService("Players") local TweenService = game:GetService("TweenService") local player = Players.LocalPlayer local screenGui = Instance.new("ScreenGui") screenGui.Parent = player:WaitForChild("PlayerGui")

-- Criando o painel principal local panel = Instance.new("Frame") panel.Size = UDim2.new(0, 300, 0, 200) panel.Position = UDim2.new(0.5, -150, 0.5, -100) panel.BackgroundColor3 = Color3.fromRGB(30, 30, 30) panel.BorderSizePixel = 0 panel.Parent = screenGui

-- Criando o botão de ocultar/exibir o painel local toggleButton = Instance.new("TextButton") toggleButton.Size = UDim2.new(0, 100, 0, 30) toggleButton.Position = UDim2.new(0.5, -50, 0, -40) toggleButton.Text = "Mostrar/Ocultar" toggleButton.Parent = screenGui

-- Criando o botão que executa o script local executeButton = Instance.new("TextButton") executeButton.Size = UDim2.new(0, 200, 0, 50) executeButton.Position = UDim2.new(0.5, -100, 0.5, -25) executeButton.Text = "Executar Teleporte" executeButton.Parent = panel

-- Função de esconder/mostrar local isVisible = true toggleButton.MouseButton1Click:Connect(function() isVisible = not isVisible panel.Visible = isVisible end)

-- Script de teleporte local teleport_table = { location1 = Vector3.new(0, 50, 0), location2 = Vector3.new(0, 0, 0) }

local tweeninfo = TweenInfo.new(2, Enum.EasingStyle.Linear)

local function bypass_teleport(destination, callback) if player.Character and player.Character:FindFirstChild("HumanoidRootPart") then local cf = CFrame.new(destination) local tween = TweenService:Create(player.Character.HumanoidRootPart, tweeninfo, {CFrame = cf}) tween:Play() tween.Completed:Connect(function() if callback then callback() end end) end end

executeButton.MouseButton1Click:Connect(function() print("Executando teleporte...") bypass_teleport(teleport_table.location1, function() bypass_teleport(teleport_table.location2) end) end)

