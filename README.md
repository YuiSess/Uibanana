if getgenv().Crystal then 
	if game.CoreGui:FindFirstChild("Crystal Hub GUI") then
		for i, v in ipairs(game.CoreGui:GetChildren()) do
			if string.find(v.Name,  "Crystal Hub") then
				v:Destroy()
			end
		end
	end
end
getgenv().Crystal = true

local DisableAnimation = game.Players.LocalPlayer.PlayerGui:FindFirstChild('TouchGui')

local UIColor = {
	["Border Color"] = Color3.fromRGB(212, 161, 255),
	["Click Effect Color"] = Color3.fromRGB(230, 230, 230),
	["Setting Icon Color"] = Color3.fromRGB(230, 230, 230),
	["Logo Image"] = "rbxassetid://135300070242371",
	["Search Icon Color"] = Color3.fromRGB(255, 255, 255),
	["Search Icon Highlight Color"] = Color3.fromRGB(212, 161, 255),
	["GUI Text Color"] = Color3.fromRGB(230, 230, 230),
	["Text Color"] = Color3.fromRGB(230, 230, 230),
	["Placeholder Text Color"] = Color3.fromRGB(178, 178, 178),
	["Title Text Color"] = Color3.fromRGB(212, 161, 255),
	["Background Main Color"] = Color3.fromRGB(43, 43, 43),
	["Background 1 Color"] = Color3.fromRGB(30,30,30),
	["Background 1 Transparency"] = 0.5,
	["Background 2 Color"] = Color3.fromRGB(90, 90, 90),
	["Background 3 Color"] = Color3.fromRGB(53, 53, 53),
	["Background Image"] = "",
	["Page Selected Color"] = Color3.fromRGB(212, 161, 255),
	["Section Text Color"] = Color3.fromRGB(212, 161, 255),
	["Section Underline Color"] = Color3.fromRGB(212, 161, 255),
	["Toggle Border Color"] = Color3.fromRGB(212, 161, 255),
	["Toggle Checked Color"] = Color3.fromRGB(230, 230, 230),
	["Toggle Desc Color"] = Color3.fromRGB(185, 185, 185),
	["Button Color"] = Color3.fromRGB(212, 161, 255),
	["Label Color"] = Color3.fromRGB(255, 46, 46),
	["Dropdown Icon Color"] = Color3.fromRGB(230, 230, 230),
	["Dropdown Selected Color"] = Color3.fromRGB(212, 161, 255),
	["Dropdown Selected Check Color"] = Color3.fromRGB(219, 64, 64),
	["Textbox Highlight Color"] = Color3.fromRGB(212, 161, 255),
	["Box Highlight Color"] = Color3.fromRGB(212, 161, 255),
	["Slider Line Color"] = Color3.fromRGB(75, 75, 75),
	["Slider Highlight Color"] = Color3.fromRGB(194, 25, 25),
	["Tween Animation 1 Speed"] = DisableAnimation and 0 or 0.25,
	["Tween Animation 2 Speed"] = DisableAnimation and 0 or 0.5,
	["Tween Animation 3 Speed"] = DisableAnimation and 0 or 0.1,
	["Text Stroke Transparency"] = .5
}

getgenv().UIColor = UIColor
getgenv().UIToggled = false

local Library = {}
local TweenService = game:GetService('TweenService')
local uis = game:GetService("UserInputService")
local RunService = game:GetService("RunService")

local Library_Function = {}
Library_Function.Gui = Instance.new('ScreenGui')
Library_Function.Gui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
Library_Function.Gui.Name = 'Crystal Hub GUI'
Library_Function.Gui.Enabled = false

Library_Function.HideGui = Instance.new('ScreenGui')
Library_Function.HideGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
Library_Function.HideGui.Name = 'Crystal Hub Btn'

local btnHide = Instance.new('TextButton', Library_Function.HideGui) 
btnHide.BackgroundTransparency = 1
btnHide.Text = ""
btnHide.AnchorPoint = Vector2.new(0, 1)
btnHide.Size = UDim2.new(0, 50, 0, 50)
btnHide.Position = UDim2.new(0, 15, 1, -15)

local btnHideFrame = Instance.new('Frame', btnHide)
btnHideFrame.AnchorPoint = Vector2.new(0, 1)
btnHideFrame.Size = UDim2.new(0, 50, 0, 50)
btnHideFrame.Position = UDim2.new(0, 0, 1, 0)
btnHideFrame.Name = "dut dit"
btnHideFrame.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
btnHideFrame.BackgroundTransparency = getgenv().UIToggled and 0 or .25

local imgHide = Instance.new('ImageLabel', btnHide)
imgHide.AnchorPoint = Vector2.new(0, 0)
imgHide.Image = getgenv().UIColor["Logo Image"]
imgHide.BackgroundTransparency = 1
imgHide.Size = UDim2.new(0, getgenv().UIToggled and 40 or 30, 0, getgenv().UIToggled and 40 or 30)
imgHide.AnchorPoint = Vector2.new(.5, .5)
imgHide.Position = UDim2.new(.5, 0, .5, 0)

local UICornerBtnHide = Instance.new("UICorner")
UICornerBtnHide.Parent = btnHideFrame
UICornerBtnHide.CornerRadius = UDim.new(1, 0)

Library.ToggleUI = function()
	getgenv().UIToggled = not getgenv().UIToggled
	local sizeXY = getgenv().UIToggled and 40 or 30
	TweenService:Create(imgHide, TweenInfo.new(DisableAnimation and 0 or .25), {
		Size = UDim2.new(0, sizeXY, 0, sizeXY)
	}):Play()
	TweenService:Create(btnHideFrame, TweenInfo.new(DisableAnimation and 0 or .25), {
		BackgroundTransparency = getgenv().UIToggled and 0 or .25
	}):Play()
	if game.CoreGui:FindFirstChild("Crystal Hub GUI") then
		for a, b in ipairs(game.CoreGui:GetChildren()) do
			if b.Name == "Crystal Hub GUI" then
				b.Enabled = getgenv().UIToggled
			end
		end
	end
end

Library.DestroyUI = function()
	if game.CoreGui:FindFirstChild("Crystal Hub GUI") then
		for i, v in ipairs(game.CoreGui:GetChildren()) do
			if string.find(v.Name,  "Crystal Hub") then
				v:Destroy()
			end
		end
	end
end

do
	local button = btnHide
	local UIS = game:GetService("UserInputService")
	
	local dragging = false
	local dragInput, dragStart, startPos
	local holdTime = 0.1
	local holdStarted = 0
	
	local function update(input)
		local delta = input.Position - dragStart
		button.Position = UDim2.new(
			startPos.X.Scale, startPos.X.Offset + delta.X,
			startPos.Y.Scale, startPos.Y.Offset + delta.Y
		)
	end
	
	local function onInputBegan(input)
		if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
			holdStarted = tick()
			dragStart = input.Position
			startPos = button.Position
	
			input.Changed:Connect(function()
				if input.UserInputState == Enum.UserInputState.End then
					dragging = false
					holdStarted = 0
				end
			end)
		end
	end
	
	local function onInputEnded(input)
		if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
			dragging = false
			holdStarted = 0
		end
	end
	
	local function onInputChanged(input)
		if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
			dragInput = input
		end
	end
	
	button.InputBegan:Connect(onInputBegan)
	button.InputEnded:Connect(onInputEnded)
	button.InputChanged:Connect(onInputChanged)
	
	RunService.RenderStepped:Connect(function()
		if holdStarted > 0 and (tick() - holdStarted >= holdTime) and not dragging then
			dragging = true
		end
	
		if dragging and dragInput then
			update(dragInput)
		end
	end)
		
end

btnHide.MouseButton1Click:Connect(function() 
	Library.ToggleUI()
end)

Library_Function.Gui.Parent = game:GetService('CoreGui')
Library_Function.HideGui.Parent = game:GetService('CoreGui')

function Library:CreateWindow(Setting)
	local TitleNameMain = "Abacaxi Hub"
	getgenv().MainDesc = Setting.Desc or ""

	local Main = Instance.new("Frame")
	local maingui = Instance.new("ImageLabel")
	local MainCorner = Instance.new("UICorner")
	local TopMain = Instance.new("Frame")
	local TextLabelMain = Instance.new("TextLabel")
	local MainContainer

	Main.Name = "Main"
	Main.Parent = Library_Function.Gui
	Main.BackgroundColor3 = Color3.fromRGB(42, 42, 42)
	Main.BackgroundTransparency = 1.000
	Main.Position = UDim2.new(0.5, 0, 0.5, 0)
	Main.AnchorPoint = Vector2.new(0.5, 0.5)
	Main.Size = UDim2.new(0, 629, 0, 359)

	local function makeDraggable(topBarObject, object)
		local dragging = nil
		local dragInput = nil
		local dragStart = nil
		local startPosition = nil
		topBarObject.InputBegan:Connect(function(input)
			if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
				dragging = true
				dragStart = input.Position
				startPosition = object.Position
				input.Changed:Connect(function()
					if input.UserInputState == Enum.UserInputState.End then
						dragging = false
					end
				end)
			end
		end)
		topBarObject.InputChanged:Connect(function(input)
			if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
				dragInput = input
			end
		end)
		uis.InputChanged:Connect(function(input)
			if input == dragInput and dragging then
				local delta = input.Position - dragStart
				object.Position = UDim2.new(startPosition.X.Scale, startPosition.X.Offset + delta.X, startPosition.Y.Scale, startPosition.Y.Offset + delta.Y)
			end
		end)
	end

	makeDraggable(Main, Main)

	maingui.Name = "maingui"
	maingui.Parent = Main
	maingui.AnchorPoint = Vector2.new(0.5, 0.5)
	maingui.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
	maingui.BackgroundTransparency = 1.000
	maingui.Position = UDim2.new(0.5, 0, 0.5, 0)
	maingui.Selectable = true
	maingui.Size = UDim2.new(1, 30, 1, 30)
	maingui.Image = "rbxassetid://8068653048"
	maingui.ScaleType = Enum.ScaleType.Slice
	maingui.SliceCenter = Rect.new(15, 15, 175, 175)
	maingui.SliceScale = 1.300
	maingui.ImageColor3 = getgenv().UIColor["Border Color"]
	maingui.ImageTransparency = 1

	MainContainer = Instance.new("ImageLabel")
	MainContainer.Name = "MainContainer"
	MainContainer.Parent = Main
	MainContainer.BackgroundColor3 = getgenv().UIColor['Background Main Color']
	MainContainer.Size = UDim2.new(1, 0, 1, 0)
	MainContainer.BackgroundTransparency = 1
	MainContainer.Image = "rbxassetid://8387197183"
	MainContainer.ImageTransparency = 0.5

	local uistr = Instance.new("UIStroke", MainContainer)
	uistr["Thickness"] = 2
	uistr["Color"] = Color3.fromRGB(171, 171, 255)
	
	MainCorner.CornerRadius = UDim.new(0, 4)
	MainCorner.Name = "MainCorner"
	MainCorner.Parent = MainContainer
	
	TopMain.Name = "TopMain"
	TopMain.Parent = MainContainer
	TopMain.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	TopMain.BackgroundTransparency = 1.000
	TopMain.Size = UDim2.new(1, 0, 0, 25)
	
	TextLabelMain.Name = "TextLabelMain"
	TextLabelMain.Parent = TopMain
	TextLabelMain.BackgroundColor3 = Color3.fromRGB(230, 230, 230)
	TextLabelMain.BackgroundTransparency = 1.000
	TextLabelMain.Position = UDim2.new(0, 0, 0, 0)
	TextLabelMain.Size = UDim2.new(1, 0, 1, 0)
	TextLabelMain.Font = Enum.Font.GothamBold
	TextLabelMain.RichText = true
	TextLabelMain.TextSize = 16.000
	TextLabelMain.TextWrapped = true
	TextLabelMain.TextXAlignment = Enum.TextXAlignment.Center
	TextLabelMain.TextColor3 = getgenv().UIColor["GUI Text Color"]
	TextLabelMain.Text = TitleNameMain

	Library_Function.Gui.Enabled = true

	return {}
end

return Library
