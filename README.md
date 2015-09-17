p=game.Players.LocalPlayer
c=p.Character
m=p:GetMouse()
Player = game:GetService("Players").LocalPlayer
mouse=Player:GetMouse()
Cha = Player.Character
mouse.KeyDown:connect(function(key)
key:lower()
if key == "e" then
	p.Character.Animate.Disabled = true
b=Instance.new("BodyVelocity",game.Players.LocalPlayer.Character.Torso)
b.MaxForce = Vector3.new(0, 50000, 0)
for i,v in pairs(p.Character:children()) do
	v.Transparency = 0.5
end
end
end)

mouse.KeyDown:connect(function(key)
key:lower()
if key == "x" then
	p.Character.Animate.Disabled = false
p.Character.Torso.BodyVelocity:remove()
for i,v in pairs(p.Character:children()) do
	v.Transparency = 0
end
end
end)
