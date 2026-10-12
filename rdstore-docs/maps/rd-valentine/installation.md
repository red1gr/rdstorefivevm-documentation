---
icon: down
---

# INSTALLATION 

{% stepper %}
{% step %}
### EXTRACT THE FILES

**EXTRACT THE CONTENTS OF THE RD MAP FROM THE COMPRESSED FILE INTO A NEW FOLDER.**
{% endstep %}

{% step %}
### MOVE TO YOUR SERVER

&#x20;**PLACE THE ENTIRE EXTRACTED FOLDER INTO YOUR SERVER’S RESOURCES DIRECTORY**
{% endstep %}

{% step %}
### START THE MLO

&#x20;**OPEN YOUR `SERVER.CFG` AND ADD THE FOLLOWING LINE**

```css
ensure [rd_maps]
```

{% hint style="warning" %}
IF YOU HAVE A DEDICATED FOLDER FOR ALL YOUR MAPS, PLACE THE MLO INSIDE IT. IF NOT, CREATE ONE TO STORE ALL ORIGEN MAPS.
{% endhint %}
{% endstep %}
{% endstepper %}
