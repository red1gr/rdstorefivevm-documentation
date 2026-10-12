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

## <mark style="color:$primary;">RUN RD-MULTIJOB</mark>

\
**TO ENSURE THE SCRIPT `RD-MULTIJOB` IS PROPERLY LOADED IN THE `SERVER.CFG`, YOU NEED TO ADD A LINE TO THE CONFIGURATION FILE THAT STARTS THE SCRIPT WHEN THE SERVER RUNS. THIS IS TYPICALLY DONE BY ADDING THE FOLLOWING LINE AT THE APPROPRIATE SECTION IN `SERVER.CFG`**

```lua
ensure rd_multijob
```

## <mark style="color:$primary;">RUN THE SQL</mark>

<details>

<summary><strong>SQL</strong></summary>

```sql
CREATE TABLE IF NOT EXISTS player_jobs (
    id INT AUTO_INCREMENT PRIMARY KEY,
    citizenid VARCHAR(60) NOT NULL,
    job_name VARCHAR(50) NOT NULL,
    grade INT DEFAULT 0
);
```

</details>

