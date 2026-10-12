---
icon: arrows-to-circle
---

# EXPORTS

## <mark style="color:$primary;">CLIENT-SIDE NOTIFY</mark>

Use this export to send styled notifications to players.

```lua
exports['rd-interactions']:SendNotify(title, message, duration, notifyType)
```

* `title` _(string)_: The title of the notification.
* `message` _(string)_: The message content.
* `duration` _(number)_: Duration in milliseconds.
* `notifyType` _(string)_: Type of notification (`info`, `success`, `error`, etc.).

***

## <mark style="color:$primary;">TEXTUI</mark>

**Show a simple text UI:**

```lua
exports['rd-interactions']:show(text, "left", "E", false)
```

* `text` _(string)_: The text to display.
* `"left"` or `"right"` _(string)_: Side of the screen where the text appears.
* `"E"` _(string)_: Key to interact (optional).
* `false` _(boolean)_: Whether to play a sound (`true` or `false`).

**Hide the text UI:**

```lua
exports['rd-interactions']:hide()
```

***

## <mark style="color:$primary;">DOORLOCK INTERACTION</mark>

**Enable an interaction at a specific coordinate:**

```lua
exports['rd-interactions']:interactON(coords, interactionType)
```

* `coords` _(vector3)_: Position of the door.
* `interactionType` _(string)_: Use `"interact_off"` or `"interact"` depending on the state or purpose.

**Disable the interaction:**

```lua
exports['rd-interactions']:interactOFF()
```

***

## <mark style="color:$primary;">SERVER-SIDE NOTIFY</mark>

Send a notification from the server side to a client:

```lua
TriggerClientEvent('rd-notify:SendNotify', source, "Title", "Message", duration, "type")
```

* `source` _(number)_: The player's server ID.
* `"Title"` _(string)_: Title of the notification.
* `"Message"` _(string)_: Content.
* `duration` _(number)_: Time in milliseconds.
* `"type"` _(string)_: Notification type.

***

## <mark style="color:$primary;">3D TEXTUI EXPORTS</mark>

Create an interactable 3D zone in the world:

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
```

* `coords`: Center position of the interaction zone.
* `distance`: How far away players can see the interaction.
* `interactDst`: How close they must be to interact.
* `name`: Unique identifier for the interaction.
* `options`: A list of available options (label + action).

AND TO REMOVE

```lua
exports['rd-interactions']:RemoveInteraction(name)
```
