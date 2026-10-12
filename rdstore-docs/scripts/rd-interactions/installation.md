---
icon: down
---

# INSTALLATION

## <mark style="color:$primary;">SCRIPT DOWNLOAD</mark>

{% content-ref url="../../guides/how-to-install-rd-asset.md" %}
[how-to-install-rd-asset.md](../../guides/how-to-install-rd-asset.md)
{% endcontent-ref %}

## <mark style="color:$primary;">DOWNLOADING DEPENDENCIES</mark>

* **THE DEPENDENCIES FOR THIS ASSET ARE MANDATORY, SO PLEASE FOLLOW THE DEPENDENCY GUIDE COMPLETELY AND USE ALL REQUIRED FILES.**
* **WHEN DOWNLOADING A DEPENDENCY, ENSURE THE FILE IS PROPERLY UNZIPPED AND DOES NOT INCLUDE `"-MAIN"` AT THE END OF ITS NAME. IF IT DOES, PLEASE REMOVE IT.**

{% embed url="https://github.com/overextended/ox_lib/releases" %}

## <mark style="color:$primary;">UPDATE ARTIFACT AND GAMEBUILD</mark>

{% content-ref url="../../guides/how-to-update-my-server.md" %}
[how-to-update-my-server.md](../../guides/how-to-update-my-server.md)
{% endcontent-ref %}

## <mark style="color:$primary;">RUN RD-INTERACTIONS</mark>

* **TO ENSURE THE SCRIPT `RD-INTERACTIONS` IS PROPERLY LOADED IN THE `SERVER.CFG`, YOU NEED TO ADD A LINE TO THE CONFIGURATION FILE THAT STARTS THE SCRIPT WHEN THE SERVER RUNS. THIS IS TYPICALLY DONE BY ADDING THE FOLLOWING LINE AT THE APPROPRIATE SECTION IN `SERVER.CFG`**

```lua
ensure rd-interactions
```

## <mark style="color:$primary;">INTEGRATION IN QBCORE, ESX AND OTHER FRAMEWORKS</mark>

<details>

<summary><strong>QBCORE</strong></summary>



📍 FOR QBCORE USERS

Setup Instructions\
🔹 DrawText Setup

```
Go to:
```

`qbcore/client/drawtext.lua`

```
Paste the following code:
```

```lua
local function hideText()
    exports['rd-interactions']:hide()
end

local function drawText(text, _)
    exports['rd-interactions']:show(text, "left", "E", false)
end

local function keyPressed()
    CreateThread(function()
        hideText()
    end)
end

RegisterNetEvent('qb-core:client:DrawText', function(text, position)
    drawText(text, position)
end)

RegisterNetEvent('qb-core:client:HideText', function()
    hideText()
end)

exports('DrawText', drawText)
exports('HideText', hideText)
exports('KeyPressed', keyPressed)
```

🔹 Notify Setup

```
Go to:
```

`qbcore/client/functions.lua`

```
Find line 171 and replace the existing Notify function with the following:
```

```lua
function QBCore.Functions.Notify(text, texttype, length, icon)
    local message = {
        action = 'notify',
        type = texttype or 'primary',
        length = length or 5000,
    }

    if type(text) == 'table' then
        message.text = text.text or 'Placeholder'
        message.caption = text.caption or 'Placeholder'
    else
        message.text = text
    end

    if icon then
        message.icon = icon
    end

    SendNUIMessage(message)
end
```

New Function:

```lua
function QBCore.Functions.Notify(text, textype, length)
    if textype == 'primary' then textype = 'info' end 
    local ttype = textype ~= nil and textype or "info"
    local length = length ~= nil and length or 5000
    exports['rd-interactions']:SendNotify("RD NOTIFY", text, length, ttype)
end
```

</details>

<details>

<summary><strong>ESX</strong></summary>



✅ FOR ESX – Notification Function (Line 156)

```lua
function ESX.ShowNotification(message, type, length)
    if GetResourceState('rd-interactions') ~= 'missing' then
        local notifyType = 'info' 
        if type == 'error' then
            notifyType = 'error'
        elseif type == 'inform' then
            notifyType = 'info'
        elseif type == 'success' then
            notifyType = 'success'
        elseif type == 'warning' then
            notifyType = 'warning'
        end

        exports['rd-interactions']:SendNotify("RD NOTIFY", message, length or 5000, notifyType)
    else
        print('[^1ERROR^7] ^5rd-interactions^7 resource not found or not started!')
    end
end
```

✅ FOR ESX – TextUI Setup (Line 160)

```lua
function ESX.TextUI(message, type)
    if GetResourceState('rd-interactions') ~= 'missing' then
        exports['rd-interactions']:show(message, "left", "E", false)
    else
        print('[^1ERROR^7] ^5rd-interactions^7 is missing or not started!')
    end
end

function ESX.HideUI()
    if GetResourceState("rd-interactions") ~= "missing" then
        exports['rd-interactions']:hide()
    else 
        print('[^1ERROR^7] ^5rd-interactions^7 is missing or not started!')
    end
end

```

</details>

<details>

<summary><strong>OTHERS</strong></summary>

#### 🔔 **Notify UI**

This shows a styled notification message on the screen.

**Syntax:**

```lua
exports['rd-interactions']:show("RD NOTIFY", text, length, ttype)
```

**Parameters:**

* `"RD NOTIFY"`: This stays as is – it defines the UI type.
* `text`: The message you want to display.
* `length`: Duration in **milliseconds** (e.g., `5000` for 5 seconds).
* `ttype`: Type of notification style (examples: `"info"`, `"error"`, `"success"`).

**Example:**

```lua
exports['rd-interactions']:show("RD NOTIFY", "You picked up a health pack!", 5000, "success")
```

***

#### 📝 **Text UI**

This is used to show a text prompt, often at the bottom left (like "Press E to interact").

**Show Text UI:**

```lua
luaCopierModifierexports['rd-interactions']:show(text, "left", "E", false)
```

**Parameters:**

* `text`: The message to display (e.g., `"Open the door"`).
* `"left"`: Position on screen (`"left"` or `"right"`).
* `"E"`: Key to show as hint (any string).
* `false`: Usually set to `false` unless using some special condition.

**Example:**

```lua
luaCopierModifierexports['rd-interactions']:show(" enter the vault", "left", "E", false)
```

**Hide Text UI:**

```lua
luaCopierModifierexports['rd-interactions']:hide()
```

This will remove the TextUI from the screen.

</details>

## <mark style="color:$primary;">DOORLOCK</mark>

<details>

<summary><strong>QB-DOORLOCK</strong></summary>



{% code fullWidth="true" %}
```lua
📄 File: qb-doorlock/client/main.lua
🔢 Line: 127

🔧 Replace this code:

local function hideNUI()
	SendNUIMessage({
		type = "setDoorText",
		enable = false
	})
	Wait(1)
end
```
{% endcode %}

✅ With this:

```lua
local function hideNUI()
    exports['rd-interactions']:interactOFF()
    Wait(0)
end
```

📄 File: qb-doorlock/client/main.lua\
🔢 Line: 103

🔧 Replace this code:

```lua
local function displayNUIText(text)
    local color = Config.ChangeColor and (closestDoor.data.locked and Config.LockedColor or Config.UnlockedColor) or Config.DefaultColor
    SendNUIMessage({
        type = "setDoorText",
        enable = true,
        text = text,
        color = color
    })
    Wait(1)
end
```

✅ With this:

```lua
local function displayNUIText(displayText, coords)
    local interactionType

    if not closestDoor.data.locked then
        interactionType = "interact"
    else
        interactionType = "interact_off"
    end

    if authorized then
        interactionType = "interact_off"
    end

    exports['rd-interactions']:interactON(coords, interactionType)
    Wait(50)
end
```

📄 File: qb-doorlock/client/main.lua\
🔢 Line: 823

🔧 Replace this code:

```lua
CreateThread(function()
	if Config.PersistentDoorStates and isLoggedIn then Wait(1000) SetupDoors() end 

	updateDoors()
	HandleDoorDebug()
	while true do
		local sleep = 100
		if isLoggedIn and canContinue then
			playerPed = PlayerPedId()
			playerCoords = GetEntityCoords(playerPed)
			if not closestDoor.id then
				local distance = #(playerCoords - lastCoords)
				if distance > 15 then
					updateDoors()
					sleep = 1000
				else
					for k in pairs(nearbyDoors) do
						local door = Config.DoorList[k]
						if door.setText and door.textCoords then
							distance = #(playerCoords - door.textCoords)
							if distance < (closestDoor.distance or 15) then
								if distance < (door.distance or door.maxDistance) then
									closestDoor = {distance = distance, id = k, data = door}
									sleep = 0
								end
							end
						end
					end
				end
			end
			if closestDoor.id then
				while isLoggedIn do
					if not paused and IsPauseMenuActive() then
						hideNUI()
						paused = true
					elseif paused then
						if not IsPauseMenuActive() then paused = false end
					else
						playerCoords = GetEntityCoords(playerPed)
						closestDoor.distance = #(closestDoor.data.textCoords - playerCoords)
						if closestDoor.distance < (closestDoor.data.distance or closestDoor.data.maxDistance) then
							local authorized = isAuthorized(closestDoor.data)
							local displayText = ""

							if not closestDoor.data.hideLabel and Config.UseDoorLabelText and closestDoor.data.doorLabel then
								displayText = closestDoor.data.doorLabel
							else
								if not closestDoor.data.locked and not authorized then
									displayText = Lang:t("general.unlocked")
								elseif not closestDoor.data.locked and authorized then
									displayText = Lang:t("general.unlocked_button")
								elseif closestDoor.data.locked and not authorized then
									displayText = Lang:t("general.locked")
								elseif closestDoor.data.locked and authorized then
									displayText = Lang:t("general.locked_button")
								end
							end

							if displayText ~= "" and (closestDoor.data.hideLabel == nil or not closestDoor.data.hideLabel) then displayNUIText(displayText) end
						else
							hideNUI()
							break
						end
					end
					Wait(100)
				end
				closestDoor = {}
				sleep = 0
			end
		end
		Wait(sleep)
	end
end)
```

✅ With this:

```lua
CreateThread(function()
    if Config.PersistentDoorStates and isLoggedIn then Wait(1000) SetupDoors() end 

    updateDoors()
    HandleDoorDebug()
    
    local lastDisplayedText = ""

    while true do
        local sleep = 100

        if isLoggedIn and canContinue then
            playerPed = PlayerPedId()
            playerCoords = GetEntityCoords(playerPed)

            if not closestDoor.id then
                local distance = #(playerCoords - lastCoords)
                if distance > 15 then
                    updateDoors()
                    sleep = 1000
                else
                    for k in pairs(nearbyDoors) do
                        local door = Config.DoorList[k]
                        if door.setText and door.textCoords then
                            distance = #(playerCoords - door.textCoords)
                            if distance < (closestDoor.distance or 15) then
                                if distance < (door.distance or door.maxDistance) then
                                    closestDoor = {distance = distance, id = k, data = door}
                                    sleep = 0
                                end
                            end
                        end
                    end
                end
            end

            if closestDoor.id then
                while isLoggedIn do
                    if not paused and IsPauseMenuActive() then
                        hideNUI()
                        lastDisplayedText = ""  -- Reset lastDisplayedText when pausing
                        paused = true
                    elseif paused then
                        if not IsPauseMenuActive() then paused = false end
                    else
                        playerCoords = GetEntityCoords(playerPed)
                        closestDoor.distance = #(closestDoor.data.textCoords - playerCoords)
                        if closestDoor.distance < (closestDoor.data.distance or closestDoor.data.maxDistance) then
                            local authorized = isAuthorized(closestDoor.data)
                            local displayText = ""

                            if not closestDoor.data.hideLabel and Config.UseDoorLabelText and closestDoor.data.doorLabel then
                                displayText = closestDoor.data.doorLabel
                            else
                                if not closestDoor.data.locked and not authorized then
                                    displayText = Lang:t("general.unlocked")
                                elseif not closestDoor.data.locked and authorized then
                                    displayText = Lang:t("general.unlocked_button")
                                elseif closestDoor.data.locked and not authorized then
                                    displayText = Lang:t("general.locked")
                                elseif closestDoor.data.locked and authorized then
                                    displayText = Lang:t("general.locked_button")
                                end
                            end

                            local coords = closestDoor.data.textCoords

                            
                            if displayText ~= lastDisplayedText and displayText ~= "" and (closestDoor.data.hideLabel == nil or not closestDoor.data.hideLabel) then
                                
                                if lastDisplayedText ~= "" then
                                    hideNUI()  
                                end
                                displayNUIText(displayText, coords)
                                lastDisplayedText = displayText 
                            end
                        else
                            if lastDisplayedText ~= "" then
                                hideNUI()
                                lastDisplayedText = ""  -- Clear lastDisplayedText when hiding NUI
                            end
                            break
                        end
                    end
                    Wait(100)
                end
                closestDoor = {}
                sleep = 0
            end
        end
        Wait(sleep)
    end
end)
```

```
```

</details>

<details>

<summary><strong>OX-DOORLOCK</strong></summary>



````lua
📄 File: ox_doorlock/client/main.lua
🔢 Line: 274

🔧 Replace this code:

```lua
CreateThread(function()
	local lockDoor = locale('lock_door')
	local unlockDoor = locale('unlock_door')
	local showUI
	local drawSprite = Config.DrawSprite

	if drawSprite then
		local sprite1 = drawSprite[0]?[1]
		local sprite2 = drawSprite[1]?[1]

		if sprite1 then
			RequestStreamedTextureDict(sprite1, true)
		end

		if sprite2 then
			RequestStreamedTextureDict(sprite2, true)
		end
	end

	local SetDrawOrigin = SetDrawOrigin
	local ClearDrawOrigin = ClearDrawOrigin
	local DrawSprite = drawSprite and DrawSprite

	while true do
		ClosestDoor = nearbyDoors[1]

		if nearbyDoorsCount > 0 then
			for i = 1, nearbyDoorsCount do
				local door = nearbyDoors[i]

				if door.distance < door.maxDistance then
					if door.distance < ClosestDoor.distance then
						ClosestDoor = door
					end

					if drawSprite and not door.hideUi then
						local sprite = drawSprite[door.state]

						if sprite then
							SetDrawOrigin(door.coords.x, door.coords.y, door.coords.z)
							DrawSprite(sprite[1], sprite[2], sprite[3], sprite[4], sprite[5], sprite[6] * ratio, sprite[7], sprite[8], sprite[9], sprite[10], sprite[11])
							ClearDrawOrigin()
						end
					end
				end
			end
		end

		if ClosestDoor and ClosestDoor.distance < ClosestDoor.maxDistance then
			if Config.DrawTextUI and not ClosestDoor.hideUi and ClosestDoor.state ~= showUI then
				lib.showTextUI(ClosestDoor.state == 0 and lockDoor or unlockDoor)
				showUI = ClosestDoor.state
			end

			if not PickingLock and IsDisabledControlJustReleased(0, 38) then
				useClosestDoor()
			end
		elseif showUI then
			lib.hideTextUI()
			showUI = nil
		end

		Wait(nearbyDoorsCount > 0 and 0 or 500)
	end
end)


````

✅ With this:

```lua

CreateThread(function()
	local lockDoor = locale('lock_door')
	local unlockDoor = locale('unlock_door')
	local showUI
	while true do
		local num = #nearbyDoors

		if num > 0 then
			local ratio = drawSprite and GetAspectRatio(true)
			for i = 1, num do
				local door = nearbyDoors[i]

				if door.distance < door.maxDistance then
					if door.distance < (ClosestDoor?.distance or 10) then
						ClosestDoor = door
					end
				end
			end
		else ClosestDoor = nil end

		if ClosestDoor and ClosestDoor.distance < ClosestDoor.maxDistance then
			if Config.DrawTextUI and not ClosestDoor.hideUi and ClosestDoor.state ~= showUI then
				lib.showTextUI(ClosestDoor.state == 0 and lockDoor or unlockDoor)
				showUI = ClosestDoor.state
				  local interactionType = ClosestDoor.state == 0 and "interact" or "interact_off"
				exports['rd-interactions']:interactON(ClosestDoor.coords, interactionType)
			end

			if not PickingLock and IsDisabledControlJustReleased(0, 38) then
				useClosestDoor()
			end
		elseif showUI then
			lib.hideTextUI()
			showUI = nil
			exports['rd-interactions']:interactOFF()
		end

		Wait(num > 0 and 0 or 500)
	end
end)
```

```
```

</details>

<details>

<summary><strong>OTHERS</strong></summary>



#### 🔧 **Using `rd-interactions` for Showing & Hiding Door Interactions**

There are **two interaction types** available in the `rd-interactions` system:

* `"interact"` – **Displays** the interaction prompt (visible to the player).
* `"interact_off"` – **Hides** or **removes** the interaction prompt.

***

#### ✅ **To SHOW the interaction**

Use this to make an interaction prompt appear at a specific location:

```lua
exports['rd-interactions']:interactON(coords, "interact")
```

* `coords`: The 3D vector location of the door or object.
* `"interact"`: The interaction type that shows the prompt.

***

#### 🚫 **To HIDE the interaction**

Use this to turn off or remove any current interaction prompt:

```lua
exports['rd-interactions']:interactOFF()
```

Or you can also pass `"interact_off"` to remove a specific type if needed:

```lua
exports['rd-interactions']:interactON(coords, "interact_off")
```

</details>

## <mark style="color:$primary;">3D TEXTUI</mark>

<details>

<summary><strong>HOW TO USE</strong></summary>

## 📌 `rd-interactions` Interaction System

This guide explains how to use the `rd-interactions` interaction exports to create world-based interactions in your resource.

***

### ✨ CreateInteraction

This export registers a world-based interaction at specific coordinates. When a player gets close, they’ll see options to interact with.

#### ✅ Syntax

````lua
exports['rd-interactions']:CreateInteraction({
    coords = vec3(x, y, z),
    distance = number,         -- (Optional) Max render/display distance
    interactDst = number,      -- Distance within which interaction can be triggered
    name = 'unique_name',      -- Unique identifier for this interaction
    options = {                -- List of interaction options
        {
            label = 'Option Label',
            action = function(entity, coords, args) 
                -- client-side logic
            end,
            -- or use event/serverEvent with args
        }
    }
})


🧩 Example 1 – Basic Teleport Interaction

```lua
    exports['rd-interactions']:CreateInteraction({
        coords = vec3(-100.3031, -1144.3539, 25.8094),
        distance = 18.0,
        interactDst = 1.0,
        name = 'name',
        options = {
            {
                label = 'Hohaaa!',
                action = function(entity, coords, args)
                    print(entity, coords, json.encode(args))
                    local ped = PlayerPedId()
                    SetEntityCoords(ped, -100.3031, -1144.3539, 26.8094)
                end,
            },
        }
    })
````

🧩 Example 2 – Multi-Option Interaction

```lua
exports['rd-interactions']:CreateInteraction({
    coords = vec3(-95.0375, -1135.0963, 25.8317),
    distance = 18.0,
    interactDst = 1.0,
    name = 'name2',
    options = {
        {
            label = 'Give Weapon to Player',
            action = function(coords, args)
                local ped = PlayerPedId()
                GiveWeaponToPed(ped, GetHashKey("WEAPON_PISTOL"), 250, false, true)
                print("Weapon given to player!")
            end,
        },
        {
            label = 'Send Client Notification',
            event = 'test:clientNotify',
            args = {"Hello, this is a test notification from the server!"},
        },
        {
            label = 'Broadcast Message to All Players',
            serverEvent = 'test:serverBroadcast',
            args = {"This is a server-wide test message!"},
        },
    }
})
```

This interaction point gives players three options:

* Equip a pistol
* Trigger a client notification
* Trigger a server-wide broadcast message

❌ RemoveInteraction\
💬 Command Example

```lua
RegisterCommand('testremove', function(source, args)
    exports['rd-interactions']:RemoveInteraction(args[1])
end, false)
```

/testremove name2

📝 Notes

coords should be a vec3.

interactDst defines the trigger radius, while distance defines the render radius.

Use action, event, or serverEvent to define behavior.

The name field must be unique per interaction.

</details>
