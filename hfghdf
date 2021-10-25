-- mw#6707
-- // Config
getgenv().Cursor = {
    Enabled = true,
    Speed = 5,
    Radius = 45,
    Color = Color3.fromRGB(180, 50, 255),
    Thickness = 1.5,
    Outline = true
}
-- // Variables
local rs = game:GetService("RunService")
--
local utility = {}
-- // Functions
function utility:new(type, properties)
    local object = Drawing.new(type)
    
    for i, v in pairs(properties) do
        object[i] = v
    end
    return object
end
-- // Initilisation
local lines = {}
-- // Drawings
local dot = utility:new("Square",{
    Visible =  true,
    Size = Vector2.new(2, 2),
    Color = getgenv().Cursor.Color,
    Filled = true,
    ZIndex = 2,
    Transparency = 1
})
--
local outline = utility:new("Square",{
    Visible =  true,
    Size = Vector2.new(4, 4),
    Color = Color3.fromRGB(0, 0, 0),
    Filled = true,
    ZIndex = 1,
    Transparency = 1
})
--
for i=1 , 4 do
    local line = utility:new("Line",{
        Visible =  true,
        From = Vector2.new(200,500),
        To = Vector2.new(200,500),
        Color = getgenv().Cursor.Color,
        Thickness = getgenv().Cursor.Thickness,
        ZIndex = 2,
        Transparency = 1
    })
    --
    local line_outline = utility:new("Line",{
        Visible =  true,
        From = Vector2.new(200,500),
        To = Vector2.new(200,500),
        Color = Color3.fromRGB(0, 0, 0),
        Thickness = getgenv().Cursor.Thickness + 2.5,
        ZIndex = 1,
        Transparency = 1
    })
    --
    lines[i] = {line, line_outline}
end
-- // Main
local angle = 0
--
local connection = rs.RenderStepped:connect(function()
    if getgenv().Cursor.Enabled then
        local pos = Vector2.new(game.Players.LocalPlayer:GetMouse().X, game.Players.LocalPlayer:GetMouse().Y + game:GetService("GuiService"):GetGuiInset().Y)
        angle = angle + (1 / (getgenv().Cursor.Speed * 10))
        --
        dot.Visible = true
        dot.Color = getgenv().Cursor.Color
        dot.Position = Vector2.new(pos.X - 1, pos.Y - 1)
        --
        outline.Visible = getgenv().Cursor.Outline
        outline.Position = Vector2.new(pos.X - 2, pos.Y - 2)
        --
        for index, line in pairs(lines) do
            index = index
            x = {pos.X + (math.cos(angle + (index * (math.pi / 2))) * (getgenv().Cursor.Radius + ((getgenv().Cursor.Radius * math.sin(angle)) / 9))), pos.X + (math.cos(angle + (index * (math.pi / 2))) * ((getgenv().Cursor.Radius - 20) - (((getgenv().Cursor.Radius - 20) * math.cos(angle)) / 4)))}
            y = {pos.Y + (math.sin(angle + (index * (math.pi / 2))) * (getgenv().Cursor.Radius + ((getgenv().Cursor.Radius * math.sin(angle)) / 9))), pos.Y + (math.sin(angle + (index * (math.pi / 2))) * ((getgenv().Cursor.Radius - 20) - (((getgenv().Cursor.Radius - 20) * math.cos(angle)) / 4)))}
            --
            line[1].Visible = true
            line[1].Color = getgenv().Cursor.Color
            line[1].From = Vector2.new(x[2], y[2])
            line[1].To = Vector2.new(x[1], y[1])
            line[1].Thickness = getgenv().Cursor.Thickness
            --
            line[2].Visible = getgenv().Cursor.Outline
            line[2].From = line[1].From
            line[2].To = line[1].To
            line[2].Thickness = getgenv().Cursor.Thickness + 2.5
        end
    else
        dot.Visible = false
        outline.Visible = false
        --
        for index, line in pairs(lines) do
            line[1].Visible = false
            line[2].Visible = false
        end
    end
end)
