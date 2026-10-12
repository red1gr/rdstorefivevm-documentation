---
icon: down
---

# INSTALLATION

## <mark style="color:$primary;">SCRIPT DOWNLOAD</mark>

{% content-ref url="../../guides/how-to-install-rd-asset.md" %}
[how-to-install-rd-asset.md](../../guides/how-to-install-rd-asset.md)
{% endcontent-ref %}

## <mark style="color:$primary;">UPDATE ARTIFACT AND GAMEBUILD</mark>

{% content-ref url="../../guides/how-to-update-my-server.md" %}
[how-to-update-my-server.md](../../guides/how-to-update-my-server.md)
{% endcontent-ref %}

## <mark style="color:$primary;">RUN SQL</mark>

<details>

<summary><strong>SQL</strong></summary>

```sql
CREATE TABLE IF NOT EXISTS rd_lockers (
    id INT AUTO_INCREMENT PRIMARY KEY,
    locker_id VARCHAR(50) NOT NULL UNIQUE,
    owner_cid VARCHAR(50) NOT NULL,
    paid BOOLEAN DEFAULT FALSE
);
CREATE TABLE IF NOT EXISTS rd_props (
    id INT AUTO_INCREMENT PRIMARY KEY,
    model VARCHAR(255) NOT NULL,
    x FLOAT NOT NULL,
    y FLOAT NOT NULL,
    z FLOAT NOT NULL,
    heading FLOAT NOT NULL
);
```

</details>

## <mark style="color:$primary;">RUN RD-LOCKERS</mark>

**TO ENSURE THE SCRIPT `RD-LOCKERS` IS PROPERLY LOADED IN THE `SERVER.CFG`, YOU NEED TO ADD A LINE TO THE CONFIGURATION FILE THAT STARTS THE SCRIPT WHEN THE SERVER RUNS. THIS IS TYPICALLY DONE BY ADDING THE FOLLOWING LINE AT THE APPROPRIATE SECTION IN `SERVER.CFG`**

```lua
ensure rd-lockers
```
