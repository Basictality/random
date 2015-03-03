x=Instance.new("ScreenGui",game.Players.LocalPlayer.PlayerGui)
x.Name = "Script Exe"
sf=Instance.new("ScrollingFrame",x)
sf.Size = UDim2.new(0,500,0,300)
sf.Position = UDim2.new(0,250,0,0)
textbox=Instance.new("TextBox",sf)
textbox.Size = UDim2.new(0, 370,0, 1500)
textbox.BackgroundColor3=Color3.new(255,255,255)
textbox.Position = UDim2.new(0,0,0,0)
textbox.TextXAlignment = "Left"
textbox.Text = "Hi"
textbox.TextYAlignment = "Top"
textbox.ClearTextOnFocus = false
textbox.MultiLine = true
textbox.FontSize = Enum.FontSize.Size14
---------
---------
button=Instance.new("TextButton",sf)
button.Size = UDim2.new(0,115,0,1500)
button.Position = UDim2.new(0,370,0,0)
button.Text="RUN"
button.BackgroundColor3 = Color3.new(0,1,0)

function onClicked(GUI)
x["Execute Script"].Value = textbox.Text
wait(0.1)
loadstring(x["Execute Script"].Value)()
end
button.MouseButton1Click:connect(onClicked)

sv=Instance.new("StringValue",x)
sv.Name = "Execute Script"
