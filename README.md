me = game.Players.LocalPlayer.Character
x=me
z=Instance.new("Part",x)
z.FormFactor = "Custom"
z.Material = "Metal"
z.Size = Vector3.new(0.1,0.5,7.5)
z.Color = Color3.new(0,0,0)

function onTouched(hit)
local human = hit.Parent:findFirstChild("Humanoid") 
if (human == nil) then return end 
human:TakeDamage(5)
end 
z.Touched:connect(onTouched)

n=Instance.new("Weld",z)
n.Part0=z
n.Part1=game.Players.LocalPlayer.Character["Right Arm"]
n.C0=CFrame.new(0,1,3.5)

wed=Instance.new("WedgePart",x)
wed.FormFactor = "Custom"
wed.Size = Vector3.new(0.3,0.5,0.5)
wed.Color = Color3.new(0,0,0)
wed.Material = "Metal"

pa=Instance.new("Part",x)
pa.FormFactor = "Custom"
pa.Size = Vector3.new(0.3,0.1,7.5)
pa.Color = Color3.new(1,0,0)

weld2=Instance.new("Weld",pa)
weld2.Part0=pa
weld2.Part1=z
weld2.C0=CFrame.new(0,0,0)

gr=Instance.new("Part",x)
gr.Size = Vector3.new(0.1,0.1,0.1)
gr.Color = Color3.new(0,0,0)
gr.Material = "Metal"


grw=Instance.new("Weld",gr)
grw.Part0=z
grw.Part1=gr
grw.C0=CFrame.new(0,0,2.5)

weld=Instance.new("Weld",wed)
weld.Part0=z
weld.Part1=wed
weld.C0=CFrame.new(0,0,-4) * CFrame.fromEulerAnglesXYZ(0,0,3.1)

me = game.Players.LocalPlayer.Character
x=me
ze=Instance.new("Part",x)
ze.FormFactor = "Custom"
ze.Material = "Metal"
ze.Size = Vector3.new(0.1,0.5,7.5)
ze.Color = Color3.new(0,0,0)

function onTouched(hit)
local human1 = hit.Parent:findFirstChild("Humanoid") 
if (human1 == nil) then return end 
human1:TakeDamage(5)
end 
ze.Touched:connect(onTouched)

ne=Instance.new("Weld",ze)
ne.Part0=ze
ne.Part1=game.Players.LocalPlayer.Character["Left Arm"]
ne.C0=CFrame.new(0,1,3.5)

wede=Instance.new("WedgePart",x)
wede.FormFactor = "Custom"
wede.Size = Vector3.new(0.3,0.5,0.5)
wede.Color = Color3.new(0,0,0)
wede.Material = "Metal"

pae=Instance.new("Part",x)
pae.FormFactor = "Custom"
pae.Size = Vector3.new(0.3,0.1,7.5)
pae.Color = Color3.new(1,0,0)

weld2e=Instance.new("Weld",pae)
weld2e.Part0=pae
weld2e.Part1=ze
weld2e.C0=CFrame.new(0,0,0)

gre=Instance.new("Part",x)
gre.Size = Vector3.new(0.1,0.1,0.1)
gre.Color = Color3.new(0,0,0)
gre.Material = "Metal"


grwe=Instance.new("Weld",gre)
grwe.Part0=ze
grwe.Part1=gre
grwe.C0=CFrame.new(0,0,2.5)

welde=Instance.new("Weld",wede)
welde.Part0=ze
welde.Part1=wede
welde.C0=CFrame.new(0,0,-4) * CFrame.fromEulerAnglesXYZ(0,0,3.1)

p=game.Players.LocalPlayer
c=p.Character
m=p:GetMouse()
Player = game:GetService("Players").LocalPlayer
mouse=Player:GetMouse()
Cha = Player.Character
mouse.KeyDown:connect(function(key)
key:lower()
if key == "e" then
me = game.Players.LocalPlayer.Character
w = Instance.new("Weld",me)
w.Part0=me.Torso
w.Part1=me['Right Arm']

me = game.Players.LocalPlayer.Character
w4 = Instance.new("Weld",me)
w4.Part0=me.Torso
w4.Part1=me['Left Arm']

for i = 59,1,-1.5 do wait()
w4.C0=CFrame.new(-1.5,0,0) * CFrame.Angles(i,0,-0.4)
w.C0=CFrame.new(1.5,0,0) * CFrame.Angles(i,0,0.4)
end
wait(0.2)
w4.C0=CFrame.new(-1.5,0,0) * CFrame.Angles(0,0,-0.4)
w.C0=CFrame.new(1.5,0,0) * CFrame.Angles(0,0,0.4)
end
end)
