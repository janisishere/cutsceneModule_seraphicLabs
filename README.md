Cutscene Module [Roblox]

<a name="top"></a>
<div align="left">
<h1>Cutscene Module V1</h1>
a module for easier cutscene creation <br>
module is still WIP!
<br>


<hr>
<sup>This is one of my first ever made Community Resources so please don't judge me. Grammar/Spelling errors may appear.</sup>
</div>
Current Version: 1.4

<h2>🔨 The Features: </h2>

* Cinematic GUI
  * These Black Squares that tween into the Screen
* Camera Manipulation
  * Supports Tweens
  * Based on Offset Rotation from a Target Part.
* Dialoges
  * with animations
* Templates and animations are easily addable
  * Animations are defined in ModuleScripts.
  * Templates are ScreenGUIs in the 'Templates' folder.
* Auto-Correction
  * The Module supports Tab-Completion & uses `setmetatable()`

## :rocket: Get started!

| 🚀 Navigation |
| --- |
| [Getting the Module](#gettingthemodule) |
| [Requiring the Module](#requiringthemodule) |
| [A Example](#example) |
| [Skip To Documentation](#documentation) |

<a name="gettingthemodule"></a>
<h2> Getting the Module </h2>
You can get the Module from the Creator Store or from this GitHub.

Then place it anywhere you want.

<a name="requiringthemodule"></a>
<h2> Requiring the Module </h2>

To require/use the module, use the following snippet:
```
local ccm = require(path.cutsceneModule) -- replace 'path' with the actual path of the module
local cutscene = ccm.new({})
```

<a name="howtouse"></a>
<h2> How to use </h2>
To begin actually using the module, you need to specify the settings.
Here's a full table of possible settings (as of V1.23):

```
ccm.new({
         targets = {Players}, -- Players affected by the cutscene

         cutscene = {
                 template = number, -- Defaults on 1
         	 time = number, -- Tween time for In()
         	 distance = number, -- GUI distance (0.5 = full screen)
         	 returnTime = number, -- Tween time for Out()
         	 delay = number, -- Delay before Out() in AutoIn()
         }

         camera = {
             targetPart = BasePart,
             offsetRotation = Vector3, -- The offset-rotation
             offsetPosition = Vector3, -- The offset-position
             rotateWithTarget = boolean, -- If the Rotation should add with the Targets Rotation
             positionWithTarget = boolean, -- If the Position should multiply with the Targets Position
         }

         dialog = {
         	 template = number, -- Defaults on 1
         	 message = {
         	 	[number] = {
         	 		beginwait = number, -- The wait-time at the beginning of the text
         	 		text = string,
         	 		animation = number, -- The Animation (Defaults on 1)
         	 		time = number, -- How long the animation should take
         	 		delay = number, -- The wait-time before the text disappears (w/ animation)
         	 		endwait = number, -- The wait-time at the end of the text
         	 	},
         	 	
                        -- After this point only use value which needed (for your cutscene)
         	 	playername = { 
         	 		text = string,
         	 		animation = number, -- The Animation (Defaults on 1)
         	 		time = number, -- How long the animation should take
         	 		delay = number, -- The wait-time before the text disappears
         	 	},
         	 },
})
```

<a name="example"></a>
<h2> A Example </h2>

Here a example how it would look like (used in the showcase):
```
-- LOCAL SCRIPT
local ccm = require(game.ReplicatedStorage.cutsceneModule)
local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()

local cutscene = ccm.new({
	targets = {player},
	
	cutscene = {
		template = 1,
		time = 1,
		distance = .2,
		returnTime = 1,
		delay = 2,
	},
	
	camera = {
		targetPart = character:WaitForChild("HumanoidRootPart"),
		offsetRotation = Vector3.new(0, 180, 0),
		offsetPosition = Vector3.new(0, 1, -5),
		rotateWithTarget = true,
		positionWithTarget = true
	},
	
	dialog = {
		template = 1,
		
		text = {
			[1] = {
				beginwait = 0,
				text = "this is a really cool showcase!",
				animation = 1,
				time = 1,
				delay = 1,
				endwait = 0,
			},
		},

		playername = {
			text = game.Players.LocalPlayer.Name,
			animation = 1,
			time = 1,
			delay = 2,
		},
	},
})

cutscene:AutoIn()
cutscene:ActivateCamera()
task.wait(1)
cutscene:StartDialog()
```

For more information look at the Documentation below.

<br>

<a name="documentation"></a>
<br>

|  |
| --- |
| [ccm.new()](#c.new) |
| [cutscene:OverrideSettings()](#c:overridesettings) |
| [cutscene:AutoIn()](#c:autoin) |
| [cutscene:In()](#c:in) |
| [cutscene:Out()](#c:out) |
| [cutscene:ActivateCamera()](#c:activatecamera) |
| [cutscene:DeactivateCamera()](#c:deactivatecamera) |
| [cutscene:Update()](#c:update) |
| [cutscene:GetCamera()](#c:getcamera) |
| [cutscene:StartDialoge()](#c:startdialoge) |
| [cutscene:Destroy()](#c:destroy) |


<h2> Functions </h2>
<hr>
<a name = "c.new"></a>

<b>`ccm.new(settingsTable)`</b>
Creates a new metatable with specified settings under the `settingsTable` variable as a table.
Find the settings table under the dropdown menu above the documentation.
This is needed for every other function.

[🚀 Jump to the Settings Table](#howtouse)

<hr>
<a name = "c:overridesettings"></a>

<b>`cutscene:OverrideSettings(settingsTable)`</b>
Overrides settings for an existing cutscene.
Does not change all settings, only the specified ones.

<hr>
<a name = "c:autoin"></a>

<b>`cutscene:AutoIn()`</b> <sub>For GUI Cinematic Bars</sub>
Automatically uses `ccm:In()` and `ccm:Out()`.
Requires all of the variables under cutscenee.

<hr>
<a name = "c:in"></a>

<b>`cutscene:In()`</b> <sub>For GUI Cinematic Bars</sub>
Tweens the Cinematic Bars In.
Requires the `time` and `distance` variable under cutscene.

<hr>
<a name = "c:out"></a>

<b>`cutscene:Out()`</b> <sub>For GUI Cinematic Bars</sub>
Tweens the Cinematic Bars Out.
Requires the `returnTime` variable under cutscene.

<hr>
<a name = "c:activatecamera"></a>

<b>`cutscene:ActivateCamera()`</b> <sub>For Camera</sub>
Activates the Camera with the according settings.
Requires `targetPart`.

<hr>
<a name = "c:deactivatecamera"></a>

<b>`cutscene:DeactivateCamera()`</b> <sub>For Camera</sub>
Sets the camera's type back to `Enum.CameraType.Custom`.

<hr>
<a name = "c:update"></a>

<b>`cutscene:Update()`</b> <sub>For Camera</sub>
Updates the cameras Position & Rotation.

<hr>
<a name = "c:getcamera"></a>

<b>`cutscene:GetCamera()`</b> <sub>For Camera</sub>
Callbacks the Camera (for Tween-Use)

<hr>
<a name = "c:startdialog"></a>

<b>`cutscene:StartDialog()`</b> <sub>For Dialog</sub>
Starts the dialog with the settings specified under the cutscene.

<hr>
<a name = "c:destroy"></a>

<b>`cutscene:Destroy()`</b>
Destroys the cutscene, including its GUIs and Parts.

<hr>
<div align="center">
<h3>🔗 Social Links 🔗</h3>
Roblox Group: <a href="https://www.roblox.com/communities/35817035/Seraphic-Labs">Seraphic Labs</a>
<br>
Roblox Profile: <a href="https://www.roblox.com/users/4045593989/profile">the_h0lysandwich</a>
<br>
Discord: <a href="https://www.discord.gg/invite/ddcgyUzqsy">Seraphic Labs</a>
</div>
