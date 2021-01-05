<!-- PROJECT LOGO -->
<br />
<p align="center">
  <a href="https://discordhub.com/profile/740698312637939824">
    <img src="https://i.imgur.com/aA8pOer.png" alt="Logo" width="80" height="80">
  </a>
  <h6 align="center">(press the icon to add my Discord)</h6>
  <h3 align="center">MT-Api v2</h3>

  <p align="center">
    Exploiting Roblox has never been as simple!
    <br />
    <a href="https://discord.gg/66ScR2EJsu"><strong>Join the Discord »</strong></a>
  </p>
</p>

## What is MT-Api?
MT-Api is an api made to simplify Roblox exploiting.
It is able to spoof over 250+ values at once without creating any additional lag.
Yes, it is a bold claim. But I wouldn't claim it unless it is true.

Even tho the name is 'mt-api' (metatable api), it does not only have features that are using metatables.
Many of the features that 3dsboy08 wrote using metatables have been rewritten to work without any mt-hooks.

## Documentation
### Initialization 
```lua
if not getgenv().MTAPIMutex then loadstring(game:HttpGet("https://raw.githubusercontent.com/KikoTheDon/MT-Api-v2/main/__source/mt-api%20v2.lua", true))() end
```
#### AddGetHook
```lua
--> Spoofs a property upon __index
Instance:AddGetHook("Name", "newName")
Instance:AddGetHook("Name", function(self)
  if getrawmetatable(game).__index(self) == "SomeDetectedName" then
    return "UnDetectedName"
  end
end)
```
#### AddSetHook
```lua
--> Spoofs a property upon __newindex
Instance:AddSetHook("WalkSpeed", 100)
Instance:AddSetHook("WalkSpeed", function(self, value)
  if value == 0 then
    return 16
  end
end)
--> Locks the value. Cannot be changed.
Instance:AddSetHook("WalkSpeed")
```
#### AddCallHook
```lua
--> Spoofs return upon __namecall
Instance:AddCallHook("FireServer", function(self, __namecall, ...)
  local a = {...}
  if a[1] == "Ban" then
    return function() end
  end
  return __namecall(self, ...)
end)
```
#### AddGlobalGetHook
```lua
--> Spoofs a property upon __index but applies for all Instances.
game:AddGlobalGetHook("WalkSpeed", function(self)
  return 100
end)
```
#### AddGlobalSetHook
```lua
--> Spoofs 
game:AddGlobalSetHook("WalkSpeed", function(self, value)
  if value == 0 then
    return 16
  end
end)
```
#### AddGlobalCallHook
```lua
--> Spoofs return upon __namecall but applies for all Instances.
game:AddGlobalGetHook("FireServer", function(self, __namecall, ...)
  if self.Name == "KickLocalPlayer" then
    return function() end
  end
  return __namecall(self, ...)
end)
```
#### AddPropertyEmulator
```lua
--> Creates a fake environment, whenever a property is read/written from the client
--> it will change those values on a separate environment.
game.Players.LocalPlayer.Character.Humanoid:AddPropertyEmulator("WalkSpeed")
```
### Gui Environment
##### Upon using these features make sure to include this code before loading the API:
```lua
function EnableApiSetting(setting)
  getgenv()[setting] = true
end
EnableApiSetting("MTAPIGui")
```
#### MouseButton1Down
```lua
--> Creates a MouseButton1Down action.
GuiButton:MouseButton1Down(<int, x>, <int, y>)
```
#### MouseButton2Down
```lua
--> Creates a MouseButton2Down action.
GuiButton:MouseButton2Down(<int, x>, <int, y>)
```
#### MouseButton1Up
```lua
--> Creates a MouseButton1Up action.
GuiButton:MouseButton1Up(<int, x>, <int, y>)
```
#### MouseButton2Up
```lua
--> Creates a MouseButton2Up action.
GuiButton:MouseButton2Up(<int, x>, <int, y>)
```
#### MouseButton1Click
```lua
--> Creates a MouseButton1Click action.
GuiButton:MouseButton1Click()
```
#### MouseButton2Click
```lua
--> Creates a MouseButton2Click action.
GuiButton:MouseButton2Click()
```
#### MouseEnter
```lua
--> Creates a MouseEnter action.
GuiButton:MouseEnter(<int, x>, <int, y>)
```
#### MouseLeave
```lua
--> Creates a MouseLeave action.
GuiButton:MouseLeave(<int, x>, <int, y>)
```
#### MouseMoved
```lua
--> Creates a MouseMoved action.
GuiButton:MouseMoved(<int, x>, <int, y>)
```

## Todo list
- [ ] Add RBXScriptSignal support. This feature has been removed because of Synapse having a really unstable support for Signals.
- [ ] Add Protosmasher support for more features.
- [ ] Add support for more famous exploits.
