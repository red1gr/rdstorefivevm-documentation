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

## <mark style="color:$primary;">RUN RD-PRIORITYSYSTEM</mark>

\
**TO ENSURE THE SCRIPT `RD-PRIORITYSYSTEM` IS PROPERLY LOADED IN THE `SERVER.CFG`, YOU NEED TO ADD A LINE TO THE CONFIGURATION FILE THAT STARTS THE SCRIPT WHEN THE SERVER RUNS. THIS IS TYPICALLY DONE BY ADDING THE FOLLOWING LINE AT THE APPROPRIATE SECTION IN `SERVER.CFG`**

```lua
ensure rd-prioritysystem
```

## <mark style="color:$primary;">SETUP THE WEBHOOK</mark>

{% hint style="warning" %}
**IF YOU WANT TO USE THE OPPORTUNITIES WHICH CAN BE GIVEN BY A WEBHOOK, THEN YOU WILL HAVE TO SET IT UP IN OUR ASSETS. YOU CAN DO THIS BY CHANGING A VALUE TO YOUR DISCORD WEBHOOK IN THE `WEBHOOK.LUA` FILE**
{% endhint %}

```lua
webhook = " "
servername = "RD STORE"
ThumbnailUrl = "https://cdn.discordapp.com/attachments/1321927690135142478/1326957470295261214/Nouveau_projet_1_1.png?ex=678150f2&is=677fff72&hm=92ec7348f64b72a326fc6a4019c66106facad4469a0bec62edab52044c4dbc4c&" 
EmbedColor = 0x00FFFF
AuthorName = "RD STORE"
RoleToTag = "<@&1321927686444154993>" -- or false 
```

{% content-ref url="../../guides/how-to-create-webhook.md" %}
[how-to-create-webhook.md](../../guides/how-to-create-webhook.md)
{% endcontent-ref %}

