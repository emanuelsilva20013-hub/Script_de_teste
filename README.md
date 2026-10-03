local P=game:GetService("Players")
local R=game:GetService("RunService")
local U=game:GetService("UserInputService")
local TW=game:GetService("TweenService")
local LG=game:GetService("Lighting")
local LP=P.LocalPlayer
local S={spd=false,spdV=50,jmp=false,jmpV=100,infJmp=false,fly=false,flyV=60,noclip=false,inv=false,esp=false,aura=false,auto=false,aim=false,aimSpeed=0.2,fov=120,alvo=nil,antiafk=true,bv=nil,bg=nil,conn=nil}
LP.Idled:Connect(function()if S.antiafk then local v=game:GetService("VirtualUser")v:CaptureController()v:ClickButton2(Vector2.new())end end)
local G=Instance.new("ScreenGui")
G.Name="DeltaHub"
G.ResetOnSpawn=false
G.IgnoreGuiInset=true
G.Parent=LP:WaitForChild("PlayerGui")
local B=Instance.new("TextButton",G)
B.Size=UDim2.new(0,50,0,50)
B.Position=UDim2.new(0,15,0.5,-25)
B.BackgroundColor3=Color3.fromRGB(30,25,45)
B.Text="≡"
B.TextColor3=Color3.fromRGB(180,140,255)
B.Font=Enum.Font.GothamBold
B.TextSize=24
B.Draggable=true
B.Active=true
Instance.new("UICorner",B).CornerRadius=UDim.new(1,0)
local bs=Instance.new("UIStroke",B)
bs.Color=Color3.fromRGB(140,90,255)
bs.Thickness=1.5
local M=Instance.new("Frame",G)
M.Size=UDim2.new(0,290,0,300)
M.Position=UDim2.new(0.5,-145,0.5,-150)
M.BackgroundColor3=Color3.fromRGB(18,16,26)
M.BorderSizePixel=0
M.Active=true
M.Draggable=true
M.Visible=false
Instance.new("UICorner",M).CornerRadius=UDim.new(0,12)
local ms=Instance.new("UIStroke",M)
ms.Color=Color3.fromRGB(90,60,160)
ms.Thickness=1.5
local H=Instance.new("Frame",M)
H.Size=UDim2.new(1,0,0,30)
H.BackgroundColor3=Color3.fromRGB(28,24,42)
H.BorderSizePixel=0
Instance.new("UICorner",H).CornerRadius=UDim.new(0,12)
local Hf=Instance.new("Frame",H)
Hf.Size=UDim2.new(1,0,0,12)
Hf.Position=UDim2.new(0,0,1,-12)
Hf.BackgroundColor3=Color3.fromRGB(28,24,42)
Hf.BorderSizePixel=0
local Ti=Instance.new("TextLabel",H)
Ti.Size=UDim2.new(1,-50,1,0)
Ti.Position=UDim2.new(0,10,0,0)
Ti.BackgroundTransparency=1
Ti.Text="DELTA MOBILE HUB"
Ti.TextColor3=Color3.fromRGB(200,170,255)
Ti.Font=Enum.Font.GothamBold
Ti.TextSize=12
Ti.TextXAlignment=Enum.TextXAlignment.Left
local Cb=Instance.new("TextButton",H)
Cb.Size=UDim2.new(0,20,0,20)
Cb.Position=UDim2.new(1,-26,0.5,-10)
Cb.BackgroundColor3=Color3.fromRGB(220,60,80)
Cb.Text="×"
Cb.TextColor3=Color3.fromRGB(255,255,255)
Cb.Font=Enum.Font.GothamBold
Cb.TextSize=14
Instance.new("UICorner",Cb).CornerRadius=UDim.new(1,0)
local TB=Instance.new("Frame",M)
TB.Size=UDim2.new(1,-16,0,24)
TB.Position=UDim2.new(0,8,0,36)
TB.BackgroundColor3=Color3.fromRGB(26,22,38)
TB.BorderSizePixel=0
Instance.new("UICorner",TB).CornerRadius=UDim.new(0,8)
local TBL=Instance.new("UIListLayout",TB)
TBL.FillDirection=Enum.FillDirection.Horizontal
TBL.Padding=UDim.new(0,3)
local PB=Instance.new("Frame",M)
PB.Size=UDim2.new(1,-16,1,-74)
PB.Position=UDim2.new(0,8,0,66)
PB.BackgroundTransparency=1
B.MouseButton1Click:Connect(function()M.Visible=not M.Visible end)
Cb.MouseButton1Click:Connect(function()M.Visible=false end)
local Tabs,Pages={},{}
local function newTab(n)
local t=Instance.new("TextButton",TB)
t.Size=UDim2.new(0,62,1,0)
t.BackgroundColor3=Color3.fromRGB(40,34,58)
t.Text=n
t.TextColor3=Color3.fromRGB(180,180,200)
t.Font=Enum.Font.GothamSemibold
t.TextSize=10
Instance.new("UICorner",t).CornerRadius=UDim.new(0,6)
local p=Instance.new("ScrollingFrame",PB)
p.Size=UDim2.new(1,0,1,0)
p.BackgroundTransparency=1
p.BorderSizePixel=0
p.ScrollBarThickness=3
p.CanvasSize=UDim2.new(0,0,0,0)
p.AutomaticCanvasSize=Enum.AutomaticSize.Y
p.Visible=false
local l=Instance.new("UIListLayout",p)
l.Padding=UDim.new(0,5)
Tabs[n]=t
Pages[n]=p
t.MouseButton1Click:Connect(function()
for k,v in pairs(Tabs)do
if k==n then
v.BackgroundColor3=Color3.fromRGB(120,80,220)
v.TextColor3=Color3.fromRGB(255,255,255)
else
v.BackgroundColor3=Color3.fromRGB(40,34,58)
v.TextColor3=Color3.fromRGB(180,180,200)
end
Pages[k].Visible=k==n
end
end)
return p
end
local pT=newTab("Player")
local cT=newTab("Combat")
local vT=newTab("Visual")
local mT=newTab("Misc")
pT.Visible=true
Tabs["Player"].BackgroundColor3=Color3.fromRGB(120,80,220)
Tabs["Player"].TextColor3=Color3.fromRGB(255,255,255)
local function Tog(par,txt,def,cb)
local r=Instance.new("Frame",par)
r.Size=UDim2.new(1,-6,0,28)
r.BackgroundColor3=Color3.fromRGB(28,24,42)
r.BorderSizePixel=0
Instance.new("UICorner",r).CornerRadius=UDim.new(0,8)
local lb=Instance.new("TextLabel",r)
lb.Size=UDim2.new(1,-50,1,0)
lb.Position=UDim2.new(0,8,0,0)
lb.BackgroundTransparency=1
lb.Text=txt
lb.TextColor3=Color3.fromRGB(220,220,235)
lb.Font=Enum.Font.Gotham
lb.TextSize=11
lb.TextXAlignment=Enum.TextXAlignment.Left
local sw=Instance.new("Frame",r)
sw.Size=UDim2.new(0,34,0,16)
sw.Position=UDim2.new(1,-42,0.5,-8)
sw.BackgroundColor3=def and Color3.fromRGB(120,80,220) or Color3.fromRGB(50,45,65)
sw.BorderSizePixel=0
Instance.new("UICorner",sw).CornerRadius=UDim.new(1,0)
local kn=Instance.new("Frame",sw)
kn.Size=UDim2.new(0,12,0,12)
kn.Position=def and UDim2.new(1,-14,0.5,-6) or UDim2.new(0,2,0.5,-6)
kn.BackgroundColor3=Color3.fromRGB(255,255,255)
kn.BorderSizePixel=0
Instance.new("UICorner",kn).CornerRadius=UDim.new(1,0)
local bt=Instance.new("TextButton",r)
bt.Size=UDim2.new(1,0,1,0)
bt.BackgroundTransparency=1
bt.Text=""
local on=def
bt.MouseButton1Click:Connect(function()
on=not on
TW:Create(kn,TweenInfo.new(0.15),{Position=on and UDim2.new(1,-14,0.5,-6) or UDim2.new(0,2,0.5,-6)}):Play()
TW:Create(sw,TweenInfo.new(0.15),{BackgroundColor3=on and Color3.fromRGB(120,80,220) or Color3.fromRGB(50,45,65)}):Play()
if cb then pcall(cb,on) end
end)
end
local function Sli(par,txt,mn,mx,def,cb)
local r=Instance.new("Frame",par)
r.Size=UDim2.new(1,-6,0,38)
r.BackgroundColor3=Color3.fromRGB(28,24,42)
r.BorderSizePixel=0
Instance.new("UICorner",r).CornerRadius=UDim.new(0,8)
local lb=Instance.new("TextLabel",r)
lb.Size=UDim2.new(1,-16,0,16)
lb.Position=UDim2.new(0,8,0,2)
lb.BackgroundTransparency=1
lb.Text=txt..": "..def
lb.TextColor3=Color3.fromRGB(220,220,235)
lb.Font=Enum.Font.Gotham
lb.TextSize=10
lb.TextXAlignment=Enum.TextXAlignment.Left
local br=Instance.new("Frame",r)
br.Size=UDim2.new(1,-16,0,8)
br.Position=UDim2.new(0,8,0,22)
br.BackgroundColor3=Color3.fromRGB(45,40,60)
br.BorderSizePixel=0
Instance.new("UICorner",br).CornerRadius=UDim.new(1,0)
local fl=Instance.new("Frame",br)
fl.Size=UDim2.new((def-mn)/(mx-mn),0,1,0)
fl.BackgroundColor3=Color3.fromRGB(140,90,255)
fl.BorderSizePixel=0
Instance.new("UICorner",fl).CornerRadius=UDim.new(1,0)
local bt=Instance.new("TextButton",br)
bt.Size=UDim2.new(1,0,1,0)
bt.BackgroundTransparency=1
bt.Text=""
local dg=false
local function upd(x)
local rl=math.clamp((x-br.AbsolutePosition.X)/br.AbsoluteSize.X,0,1)
local v=math.floor((mn+(mx-mn)*rl)*100)/100
fl.Size=UDim2.new(rl,0,1,0)
lb.Text=txt..": "..v
if cb then pcall(cb,v) end
end
bt.InputBegan:Connect(function(i)
if i.UserInputType==Enum.UserInputType.MouseButton1 or i.UserInputType==Enum.UserInputType.Touch then
dg=true
upd(i.Position.X)
end
end)
U.InputChanged:Connect(function(i)
if dg and (i.UserInputType==Enum.UserInputType.MouseMovement or i.UserInputType==Enum.UserInputType.Touch) then
upd(i.Position.X)
end
end)
U.InputEnded:Connect(function(i)
if i.UserInputType==Enum.UserInputType.MouseButton1 or i.UserInputType==Enum.UserInputType.Touch then
dg=false
end
end)
end
local function Btn(par,txt,cb)
local b=Instance.new("TextButton",par)
b.Size=UDim2.new(1,-6,0,28)
b.BackgroundColor3=Color3.fromRGB(60,44,100)
b.Text=txt
b.TextColor3=Color3.fromRGB(230,220,255)
b.Font=Enum.Font.GothamSemibold
b.TextSize=11
Instance.new("UICorner",b).CornerRadius=UDim.new(0,8)
b.MouseButton1Click:Connect(function()if cb then pcall(cb) end end)
end
Tog(pT,"Speed Hack",false,function(v)
S.spd=v
local c=LP.Character
if c and c:FindFirstChildOfClass("Humanoid") then
c.Humanoid.WalkSpeed=v and S.spdV or 16
end
end)
Sli(pT,"Speed Value",16,500,50,function(v)
S.spdV=v
if S.spd then
local c=LP.Character
if c and c:FindFirstChildOfClass("Humanoid") then
c.Humanoid.WalkSpeed=v
end
end
end)
Tog(pT,"Jump Power",false,function(v)
S.jmp=v
local c=LP.Character
if c and c:FindFirstChildOfClass("Humanoid") then
c.Humanoid.UseJumpPower=true
c.Humanoid.JumpPower=v and S.jmpV or 50
end
end)
Sli(pT,"Jump Value",50,500,100,function(v)
S.jmpV=v
if S.jmp then
local c=LP.Character
if c and c:FindFirstChildOfClass("Humanoid") then
c.Humanoid.UseJumpPower=true
c.Humanoid.JumpPower=v
end
end
end)
Tog(pT,"Infinite Jump",false,function(v)S.infJmp=v end)
Sli(pT,"Fly Speed",20,300,60,function(v)S.flyV=v end)
Tog(pT,"Fly",false,function(v)
S.fly=v
local c=LP.Character
local h=c and c:FindFirstChild("HumanoidRootPart")
if not h then return end
if v then
local bv=Instance.new("BodyVelocity",h)
bv.MaxForce=Vector3.new(1e5,1e5,1e5)
bv.Velocity=Vector3.zero
local bg=Instance.new("BodyGyro",h)
bg.MaxTorque=Vector3.new(1e5,1e5,1e5)
bg.P=1000
bg.D=50
bg.CFrame=h.CFrame
S.bv=bv
S.bg=bg
S.conn=R.RenderStepped:Connect(function()
if not S.fly or not h.Parent then return end
local d=Vector3.zero
local cm=workspace.CurrentCamera
if U:IsKeyDown(Enum.KeyCode.W) then d+=cm.CFrame.LookVector end
if U:IsKeyDown(Enum.KeyCode.S) then d-=cm.CFrame.LookVector end
if U:IsKeyDown(Enum.KeyCode.A) then d-=cm.CFrame.RightVector end
if U:IsKeyDown(Enum.KeyCode.D) then d+=cm.CFrame.RightVector end
if U:IsKeyDown(Enum.KeyCode.Space) then d+=Vector3.new(0,1,0) end
if U:IsKeyDown(Enum.KeyCode.LeftShift) then d-=Vector3.new(0,1,0) end
if d.Magnitude>0 then d=d.Unit end
bv.Velocity=d*S.flyV
bg.CFrame=cm.CFrame
end)
else
if S.conn then S.conn:Disconnect() S.conn=nil end
if S.bv then S.bv:Destroy() S.bv=nil end
if S.bg then S.bg:Destroy() S.bg=nil end
end
end)
Tog(pT,"Noclip",false,function(v)S.noclip=v end)
Tog(cT,"Kill Aura",false,function(v)S.aura=v end)
Tog(cT,"Aimbot",false,function(v)
S.aim=v
if not v then S.alvo=nil end
end)
Sli(cT,"Aim Speed",0.05,1,0.2,function(v)S.aimSpeed=v end)
Sli(cT,"FOV Size",30,400,120,function(v)S.fov=v end)
Tog(cT,"Auto Clicker",false,function(v)
S.auto=v
if v then
task.spawn(function()
while S.auto do
local vu=game:GetService("VirtualUser")
vu:CaptureController()
vu:ClickButton1(Vector2.new(0,0))
task.wait(0.1)
end
end)
end
end)
Btn(cT,"Kill All (Touch)",function()
local c=LP.Character
if not c then return end
for _,pl in ipairs(P:GetPlayers()) do
if pl~=LP and pl.Character then
local t=pl.Character:FindFirstChild("HumanoidRootPart")
if t then
local o=c.HumanoidRootPart.CFrame
c.HumanoidRootPart.CFrame=t.CFrame
task.wait(0.05)
c.HumanoidRootPart.CFrame=o
end
end
end
end)
Tog(vT,"ESP",false,function(v)
S.esp=v
if not v then
for _,pl in ipairs(P:GetPlayers()) do
if pl.Character then
local h=pl.Character:FindFirstChild("HumanoidRootPart")
if h then
local e=h:FindFirstChild("ESP")
if e then e:Destroy() end
end
end
end
end
end)
Tog(vT,"Invisibility",false,function(v)
S.inv=v
local c=LP.Character
if c then
for _,x in ipairs(c:GetDescendants()) do
if x:IsA("BasePart") and x.Name~="HumanoidRootPart" then
x.LocalTransparencyModifier=v and 1 or 0
end
end
end
end)
Tog(vT,"Fullbright",false,function(v)
S.fb=v
if v then
LG.Brightness=3
LG.ClockTime=12
LG.FogEnd=1e6
LG.GlobalShadows=false
else
LG.Brightness=2
LG.GlobalShadows=true
end
end)
Tog(mT,"Anti-AFK",true,function(v)S.antiafk=v end)
Btn(mT,"Reset Character",function()
local c=LP.Character
if c and c:FindFirstChildOfClass("Humanoid") then
c.Humanoid.Health=0
end
end)
Btn(mT,"Copy JobId",function()
if setclipboard then setclipboard(game.JobId) end
end)
Btn(mT,"Destroy UI",function()G:Destroy() end)
local fov=Instance.new("Frame",G)
fov.Size=UDim2.new(0,120,0,120)
fov.Position=UDim2.new(0.5,0,0.5,0)
fov.AnchorPoint=Vector2.new(0.5,0.5)
fov.BackgroundTransparency=1
fov.ZIndex=5
fov.Visible=false
Instance.new("UICorner",fov).CornerRadius=UDim.new(1,0)
local fs=Instance.new("UIStroke",fov)
fs.Color=Color3.fromRGB(140,90,255)
fs.Thickness=1.5
fs.Transparency=0.3
R.RenderStepped:Connect(function()
fov.Size=UDim2.new(0,S.fov,0,S.fov)
fov.Visible=S.aim
if S.noclip then
local c=LP.Character
if c then
for _,x in ipairs(c:GetDescendants()) do
if x:IsA("BasePart") then x.CanCollide=false end
end
end
end
if S.infJmp then
local c=LP.Character
if c then
local h=c:FindFirstChildOfClass("Humanoid")
if h and h:GetState()~=Enum.HumanoidStateType.Jumping and h:GetState()~=Enum.HumanoidStateType.Freefall then
h:ChangeState(Enum.HumanoidStateType.Jumping)
end
end
end
if S.aura then
local c=LP.Character
if c and c:FindFirstChild("HumanoidRootPart") then
for _,pl in ipairs(P:GetPlayers()) do
if pl~=LP and pl.Character then
local h=pl.Character:FindFirstChild("HumanoidRootPart")
if h and (h.Position-c.HumanoidRootPart.Position).Magnitude<20 then
h.CFrame=c.HumanoidRootPart.CFrame*CFrame.new(0,0,-2)
end
end
end
end
end
if S.esp then
for _,pl in ipairs(P:GetPlayers()) do
if pl~=LP and pl.Character then
local h=pl.Character:FindFirstChild("HumanoidRootPart")
if h and not h:FindFirstChild("ESP") then
local bb=Instance.new("BillboardGui",h)
bb.Name="ESP"
bb.Size=UDim2.new(0,80,0,28)
bb.AlwaysOnTop=true
local t=Instance.new("TextLabel",bb)
t.Size=UDim2.new(1,0,1,0)
t.BackgroundTransparency=1
t.Text=pl.Name
t.TextColor3=Color3.fromRGB(255,90,90)
t.TextStrokeTransparency=0
t.Font=Enum.Font.GothamBold
t.TextSize=12
end
end
end
end
if S.aim then
local cm=workspace.CurrentCamera
local ct=Vector2.new(cm.ViewportSize.X/2,cm.ViewportSize.Y/2)
local rd=S.fov/2
local function val(t)
if not t or not t.Parent then return false end
local pl=P:GetPlayerFromCharacter(t.Parent)
if not pl or pl==LP then return false end
local hum=t.Parent:FindFirstChildOfClass("Humanoid")
if not hum or hum.Health<=0 then return false end
local pos,on=cm:WorldToViewportPoint(t.Position)
if not on then return false end
return (Vector2.new(pos.X,pos.Y)-ct).Magnitude<=rd
end
if not val(S.alvo) then
S.alvo=nil
local best,bd=nil,math.huge
for _,pl in ipairs(P:GetPlayers()) do
if pl~=LP and pl.Character then
local h=pl.Character:FindFirstChild("HumanoidRootPart")
local hum=pl.Character:FindFirstChildOfClass("Humanoid")
if h and hum and hum.Health>0 then
local pos,on=cm:WorldToViewportPoint(h.Position)
if on then
local d=(Vector2.new(pos.X,pos.Y)-ct).Magnitude
if d<=rd and d<bd then
bd=d
best=h
end
end
end
end
end
S.alvo=best
end
if S.alvo and S.alvo.Parent then
local goal=CFrame.new(cm.CFrame.Position,S.alvo.Position)
cm.CFrame=cm.CFrame:Lerp(goal,S.aimSpeed)
end
end
end)
print("[Delta Hub] Carregado!")
