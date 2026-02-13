if getgenv().Crystal then 
	if game.CoreGui:FindFirstChild("Crystal Hub GUI") then
		for i, v in ipairs(game.CoreGui:GetChildren()) do
			if string.find(v.Name, "Crystal Hub") then
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

local ScreenGui = Instance.new('ScreenGui')
ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
ScreenGui.Name = 'Crystal Hub GUI'
ScreenGui.Parent = game:GetService('CoreGui')

local Main = Instance.new("Frame")
Main.Name = "Main"
Main.Parent = ScreenGui
Main.BackgroundColor3 = Color3.fromRGB(42, 42, 42)
Main.BackgroundTransparency = 1.000
Main.Position = UDim2.new(0.5, 0, 0.5, 0)
Main.AnchorPoint = Vector2.new(0.5, 0.5)
Main.Size = UDim2.new(0, 629, 0, 359)

local MainContainer = Instance.new("ImageLabel")
MainContainer.Name = "MainContainer"
MainContainer.Parent = Main
MainContainer.BackgroundColor3 = UIColor['Background Main Color']
MainContainer.Size = UDim2.new(1, 0, 1, 0)
MainContainer.BackgroundTransparency = 1
MainContainer.Image = "rbxassetid://8387197183"
MainContainer.ImageTransparency = 0.5

local MainCorner = Instance.new("UICorner")
MainCorner.CornerRadius = UDim.new(0, 4)
MainCorner.Parent = MainContainer

local UIStroke = Instance.new("UIStroke", MainContainer)
UIStroke.Thickness = 2
UIStroke.Color = Color3.fromRGB(171, 171, 255)

local TopMain = Instance.new("Frame")
TopMain.Name = "TopMain"
TopMain.Parent = MainContainer
TopMain.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
TopMain.BackgroundTransparency = 1.000
TopMain.Size = UDim2.new(1, 0, 0, 25)

local TextLabelMain = Instance.new("TextLabel")
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
TextLabelMain.TextColor3 = UIColor["GUI Text Color"]
TextLabelMain.Text = "Nawy Hub"

print("UI carregada com sucesso!")
