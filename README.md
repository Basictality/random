--If doesn't work go to https://code.stypi.com/raw/commandercornbread/jetboots

plyr = game.Players.LocalPlayer
mouse = plyr:GetMouse()


NewRS = nil
boost = nil
gyro = nil
isfloating = false
charging = false
maxfuel = 500
fuel = maxfuel
charge_int = .5
maxTrq = Vector3.new(7000, .01, 7000)
origPow = Instance.new("BodyGyro").P
speed = 0
maxspd = 1000

shoecol = BrickColor.Random().Name

leftboot = Instance.new("Part", plyr.Character)
leftboot.FormFactor = "Custom"
leftboot.Size = Vector3.new(1.1, 1.1, 1.1)
leftboot.BottomSurface = "Inlet"
leftboot.CanCollide = false
leftboot.BrickColor = BrickColor.new(shoecol)

rightboot = leftboot:Clone()
rightboot.Parent = leftboot.Parent
rbweld = Instance.new("Weld", rightboot)
rbweld.Part0 = rightboot
rbweld.Part1 = plyr.Character["Right Leg"]
rbweld.C0 = CFrame.new(0, .5, 0)
lbweld = Instance.new("Weld", leftboot)
lbweld.Part0 = leftboot
lbweld.Part1 = plyr.Character["Left Leg"]
lbweld.C0 = CFrame.new(0, .5, 0)

screen = Instance.new("Part", leftboot.Parent)
screen.Name = "Screen"
screen.FormFactor = "Custom"
screen.Size = Vector3.new(.2, 1, 2)
screen.Transparency = 1
screen.CanCollide = false
scweld = Instance.new("Weld", screen)
scweld.Part0 = screen
scweld.Part1 = rightboot
scweld.C0 = CFrame.new(-.6, -.2, 0)

surf = Instance.new("SurfaceGui", screen)
surf.Face = "Right"
surf.CanvasSize = Vector2.new(200,150)
lab = Instance.new("TextLabel", surf)
lab.Size = UDim2.new(0, 0, 0, 0)
lab.Position = UDim2.new(.5, 0, .5, 0)
lab.BackgroundColor3 = Color3.new(176/255,196/255,252/255) --Color3.new(.6, .6, .6)
lab.BackgroundTransparency = .8
lab.FontSize = "Size48"
lab.Text = "100%"
lab.BorderSizePixel = 0
lab.TextColor3 = Color3.new(1,1,1)
lab.ClipsDescendants = true

NewRS = nil
NewLS = nil

lfire = nil
rfire = nil

function startfloat()

	if gyro then
		gyro:Destroy()
	end
	
	char = plyr.Character
	ra = char:FindFirstChild("Right Arm")
	la = char:FindFirstChild("Left Arm")
	torso = char.Torso
	char.Humanoid.PlatformStand = true
	
	if ra then
		torso["Right Shoulder"].Part0 = nil
		torso["Right Shoulder"].Part1 = nil
		torso["Right Shoulder"].Name = "RSBlank"

		NewRS = Instance.new("Weld", torso)
		NewRS.Name = "Control Right Shoulder"
		
		--ra.Name = "RA"
		ra.TopSurface = "Smooth"
		
		NewRS.Part0 = torso
		NewRS.Part1 = ra
		
		NewRS.C0 = CFrame.new(1.5, .5, 0) * CFrame.Angles(0, math.rad(-20), math.rad(40)) * CFrame.new(0, -.25, 0)
	end
	
	if la then
		torso["Left Shoulder"].Part0 = nil
		torso["Left Shoulder"].Part1 = nil
		torso["Left Shoulder"].Name = "LSBlank"

		NewLS = Instance.new("Weld", torso)
		NewLS.Name = "Control Left Shoulder"
		
		--la.Name = "LA"
		la.TopSurface = "Smooth"
		
		NewLS.Part0 = torso
		NewLS.Part1 = la
		
		NewLS.C0 = CFrame.new(-1.5, .5, 0) * CFrame.Angles(0, math.rad(20), math.rad(-40)) * CFrame.new(0, -.25, 0)
	end

	
	boost = Instance.new("BodyVelocity", torso)
	boost.velocity = Vector3.new(0, 5, 0)
	boost.maxForce = Vector3.new(5500, 10000--[[6000]], 5500)
	
	gyro = Instance.new("BodyGyro", torso)
	gyro.cframe = torso.CFrame * CFrame.Angles(math.rad(-3), 0, 0)
	gyro.maxTorque = maxTrq
	
	rfire = Instance.new("Fire", rightboot)
	rfire.Size = 2.5
	rfire.Heat = -10

	lfire = rfire:Clone()
	lfire.Parent = leftboot
	
	
	isfloating = true
	--ns = torso.Neck
end

function floatforward()
	while gyro.Parent ~= nil and boost.Parent ~= nil do
		gyro.cframe = gyro.cframe 
	end
end

function float()
	speed = 0
	repeat
		if keylist['w'] then
		    gyro.maxTorque = maxTrq
		    gyro.P = origPow
			
			gyro.cframe = CFrame.new(torso.Position, mouse.Hit.p) * CFrame.Angles(math.rad(-90), 0, 0)
			
			lfire.Heat = -15
			rfire.Heat = -15
			
			if speed >= maxspd then
			    lfire.Size = 5
			    rfire.Size = 5
			else
			    lfire.Size = 2.5
			    rfire.Size = 2.5
			end
			
			if speed < maxspd then speed = speed + 1 end
			boost.velocity = CFrame.new(torso.Position, mouse.Hit.p).lookVector * speed

		else
		    if speed > 0 then speed = speed - 3 end
		    
            gyro.maxTorque = Vector3.new(maxTrq.x, 0, 0)
            gyro.P = origPow
            
			gyro.cframe = CFrame.new(torso.Position) * CFrame.Angles(math.rad(-3), 0, 0)
			boost.velocity = Vector3.new(0, 2, 0)
		end
		wait()
		fuel = fuel - .5
	until fuel <= 0 or not keylist["g"]
end

function stopfloat()
	
	--torso.Neck.C0 = CFrame.new(0, 1, 0, -1, -0, -0, 0, 0, 1, 0, 1, 0)
	if NewRS then
		NewRS:Destroy()
		ra.Name = "Right Arm"
	end
	if NewLS then
		NewLS:Destroy()
		la.Name = "Left Arm"
	end
	
	if char.Torso:FindFirstChild("RSBlank") then
		rsweld = char.Torso.RSBlank
		rsweld.Name = "Right Shoulder"
		rsweld.Part0 = torso
		rsweld.Part1 = ra
	end
	if char.Torso:FindFirstChild("LSBlank") then
		lsweld = char.Torso.LSBlank
		lsweld.Name = "Left Shoulder"
		lsweld.Part0 = torso
		lsweld.Part1 = la
	end
	
	char.Humanoid.PlatformStand = false
	
	if boost then
		boost:Destroy()
	end
	if gyro then
		gyro:Destroy()
	end
	
	if rfire then rfire:Destroy() end
	if lfire then lfire:Destroy() end
	
	isfloating = false
end


function Recharge()
	coroutine.resume(coroutine.create(function()
		charging = true
		char = plyr.Character
		lab:TweenSizeAndPosition(UDim2.new(1, 0, 1, 0), UDim2.new(0, 0, 0, 0), "Out", "Linear", .7, true)
		local con = char.Humanoid.Running:connect(function(spd)
			if spd > 0 then
				lab:TweenSizeAndPosition(UDim2.new(0, 0, 0, 0), UDim2.new(.5, 0, .5, 0), "Out", "Linear", .7, true)
			end
			wait()
			if spd <= 0 then
				lab:TweenSizeAndPosition(UDim2.new(1, 0, 1, 0), UDim2.new(0, 0, 0, 0), "Out", "Linear", .7, true)
			end
		end)
		repeat
			fuel = fuel + charge_int
			lab.Text = math.floor(100*(fuel/maxfuel)).."%"
			wait()
		until fuel >= maxfuel or isfloating
		lab:TweenSizeAndPosition(UDim2.new(0, 0, 0, 0), UDim2.new(.5, 0, .5, 0), "Out", "Linear", .7, true)
		con:disconnect()
		charging = false
	end))
end

function RunThru()
    --plyr.Character.Humanoid.Jump = true
	pcall(function() startfloat() end)
	
	float()
	
	stopfloat()

	if not charging then Recharge() end
end


keylist = {}
mouse.KeyDown:connect(function(key)
	keylist[key] = true
	
	if key == "g" then
		RunThru()
	elseif key == "w" then
	end
		
end)

mouse.KeyUp:connect(function(key)
	keylist[key] = nil
end)


debounce = false
plyr.Character.Head.Touched:connect(function(hit)
    if hit.Parent:FindFirstChild("Humanoid") and speed >= maxspd and not debounce then
        debounce = true
        guy = hit.Parent
        guy.Humanoid.PlatformStand = true
        local bf = Instance.new("BodyForce", guy.Torso)
        bf.force = CFrame.new(plyr.Character.Head.Position, hit.Parent.Torso.Position).lookVector * 500
        wait(.5)
        bf:Destroy()
        guy.Humanoid.PlatformStand = false
        wait(.5)
        debounce = false
    end
end)




