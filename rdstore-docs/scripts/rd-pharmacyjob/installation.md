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

## <mark style="color:$primary;">RUN RD-PHARMACYJOB</mark>

\
**TO ENSURE THE SCRIPT `RD-PHARMACYJOB` IS PROPERLY LOADED IN THE `SERVER.CFG`, YOU NEED TO ADD A LINE TO THE CONFIGURATION FILE THAT STARTS THE SCRIPT WHEN THE SERVER RUNS. THIS IS TYPICALLY DONE BY ADDING THE FOLLOWING LINE AT THE APPROPRIATE SECTION IN `SERVER.CFG`**

```lua
ensure rd-pharmacyjob
```

## <mark style="color:$primary;">INTEGRATION IN QBCORE, ESX AND OTHER FRAMEWORKS</mark>

## THE PHARMACY JOB

<details>

<summary>QBCORE</summary>

{% hint style="info" %}
go to qb-core/shared/jobs.lua
{% endhint %}

Add your job like this:

```lua
['pharmacy'] = {
    label = 'Pharmacy',
    defaultDuty = true,
    offDutyPay = false,
    grades = {
        ['0'] = { name = 'recruit', label = 'Recruit', payment = 200 },
        ['1'] = { name = 'worker', label = 'Worker', payment = 300 },
        ['2'] = { name = 'supervisor', label = 'Supervisor', payment = 400 },
        ['3'] = { name = 'boss', label = 'Boss', isboss = true, payment = 500 },
    }
}
```



</details>

<details>

<summary>ESX</summary>

{% hint style="info" %}
upload this sql
{% endhint %}

```sql
INSERT INTO jobs (name, label) VALUES ('pharmacy', 'Pharmacy');
INSERT INTO job_grades (job_name, grade, name, label, salary, skin_male, skin_female)
VALUES
('pharmacy', 0, 'recruit', 'Recruit', 200, '{}', '{}'),
('pharmacy', 1, 'employee', 'Employee', 300, '{}', '{}'),
('pharmacy', 2, 'supervisor', 'Supervisor', 400, '{}', '{}'),
('pharmacy', 3, 'boss', 'Boss', 500, '{}', '{}');
```

</details>

<details>

<summary>QBOX</summary>

{% hint style="info" %}
qbx\_core/shared/jobs.lua
{% endhint %}

Add your job like this:

```lua
['pharmacy'] = {
    label = 'Pharmacy',
    defaultDuty = true,
    offDutyPay = false,
    grades = {
        [0] = { name = 'recruit', label = 'Recruit', payment = 200 },
        [1] = { name = 'employee', label = 'Employee', payment = 300 },
        [2] = { name = 'manager', label = 'Manager', payment = 400 },
        [3] = { name = 'boss', label = 'Boss', isboss = true, payment = 500 },
    }
}

```

</details>

## ITEMS

{% hint style="danger" %}
If you don't have the items integrated correctly, you will receive random errors.
{% endhint %}

{% hint style="success" %}
Check that you don't have duplicate items in your inventory or database before integrating them, otherwise you might have some errors.
{% endhint %}

<details>

<summary>QBCORE</summary>

<pre class="language-lua"><code class="lang-lua"><strong>    -- Base Ingredients
</strong>['chemical'] = { name = 'chemical', label = 'Chemical', weight = 100, type = 'item', image = 'chemical.png', unique = false, useable = false, shouldClose = true, combinable = nil, description = 'A chemical base for creating medicine.' },
['alcohol'] = { name = 'alcohol', label = 'Alcohol', weight = 100, type = 'item', image = 'alcohol.png', unique = false, useable = false, shouldClose = true, combinable = nil, description = 'Used for disinfection or mixing medicine.' },
['water'] = { name = 'water', label = 'Purified Water', weight = 100, type = 'item', image = 'water.png', unique = false, useable = false, shouldClose = true, combinable = nil, description = 'Purified water used for chemical mixtures.' },
['herbs'] = { name = 'herbs', label = 'Herbs', weight = 100, type = 'item', image = 'herbs.png', unique = false, useable = false, shouldClose = true, combinable = nil, description = 'Medicinal herbs for natural remedies.' },
['sugar'] = { name = 'sugar', label = 'Sugar', weight = 100, type = 'item', image = 'sugar.png', unique = false, useable = false, shouldClose = true, combinable = nil, description = 'Sweet crystalline substance used in mixtures.' },

-- Medicine Recipes
['doliprane'] = { name = 'doliprane', label = 'Doliprane', weight = 100, type = 'item', image = 'doliprane.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Pain relief medication.' },
['dstress'] = { name = 'dstress', label = 'Dstress', weight = 100, type = 'item', image = 'dstress.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Calming medicine for stress.' },
['flexen'] = { name = 'flexen', label = 'Flexen', weight = 100, type = 'item', image = 'flexen.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Anti-inflammatory medicine.' },
['glycogen'] = { name = 'glycogen', label = 'Glycogen', weight = 100, type = 'item', image = 'glycogen.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Energy supplement.' },
['nicardipine'] = { name = 'nicardipine', label = 'Nicardipine', weight = 100, type = 'item', image = 'nicardipine.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Cardiovascular medicine.' },
['rhumix'] = { name = 'rhumix', label = 'Rhumix', weight = 100, type = 'item', image = 'rhumix.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Cold relief medicine.' },
['diclo'] = { name = 'diclo', label = 'Diclo', weight = 100, type = 'item', image = 'diclo.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Painkiller and anti-inflammatory.' },

</code></pre>

</details>

<details>

<summary>ESX</summary>

```sql
INSERT INTO `items` (`name`, `label`, `weight`, `rare`, `can_remove`, `type`) VALUES
('chemical', 'Chemical', 100, 0, 1, 'item_standard'),
('alcohol', 'Alcohol', 100, 0, 1, 'item_standard'),
('water', 'Purified Water', 100, 0, 1, 'item_standard'),
('herbs', 'Herbs', 100, 0, 1, 'item_standard'),
('sugar', 'Sugar', 100, 0, 1, 'item_standard'),
('doliprane', 'Doliprane', 100, 0, 1, 'item_standard'),
('dstress', 'Dstress', 100, 0, 1, 'item_standard'),
('flexen', 'Flexen', 100, 0, 1, 'item_standard'),
('glycogen', 'Glycogen', 100, 0, 1, 'item_standard'),
('nicardipine', 'Nicardipine', 100, 0, 1, 'item_standard'),
('rhumix', 'Rhumix', 100, 0, 1, 'item_standard'),
('diclo', 'Diclo', 100, 0, 1, 'item_standard');
```

</details>

<details>

<summary>OX INVENTORY</summary>

```lua
['chemical'] = {
    label = 'Chemical',
    weight = 100,
    stack = true,
    close = true,
    description = 'A chemical base for creating medicine.',
    client = { image = 'chemical.png' }
},

['alcohol'] = {
    label = 'Alcohol',
    weight = 100,
    stack = true,
    close = true,
    description = 'Used for disinfection or mixing medicine.',
    client = { image = 'alcohol.png' }
},

['water'] = {
    label = 'Purified Water',
    weight = 100,
    stack = true,
    close = true,
    description = 'Purified water used for chemical mixtures.',
    client = { image = 'water.png' }
},

['herbs'] = {
    label = 'Herbs',
    weight = 100,
    stack = true,
    close = true,
    description = 'Medicinal herbs for natural remedies.',
    client = { image = 'herbs.png' }
},

['sugar'] = {
    label = 'Sugar',
    weight = 100,
    stack = true,
    close = true,
    description = 'Sweet crystalline substance used in mixtures.',
    client = { image = 'sugar.png' }
},

--  Medicine Recipes
['doliprane'] = {
    label = 'Doliprane',
    weight = 100,
    stack = true,
    close = true,
    description = 'Pain relief medicine.',
    client = { image = 'doliprane.png' }
},

['dstress'] = {
    label = 'Dstress',
    weight = 100,
    stack = true,
    close = true,
    description = 'Calming medicine for stress.',
    client = { image = 'dstress.png' }
},

['flexen'] = {
    label = 'Flexen',
    weight = 100,
    stack = true,
    close = true,
    description = 'Anti-inflammatory medicine.',
    client = { image = 'flexen.png' }
},

['glycogen'] = {
    label = 'Glycogen',
    weight = 100,
    stack = true,
    close = true,
    description = 'Energy supplement.',
    client = { image = 'glycogen.png' }
},

['nicardipine'] = {
    label = 'Nicardipine',
    weight = 100,
    stack = true,
    close = true,
    description = 'Cardiovascular medicine.',
    client = { image = 'nicardipine.png' }
},

['rhumix'] = {
    label = 'Rhumix',
    weight = 100,
    stack = true,
    close = true,
    description = 'Cold relief medicine.',
    client = { image = 'rhumix.png' }
},

['diclo'] = {
    label = 'Diclo',
    weight = 100,
    stack = true,
    close = true,
    description = 'Painkiller and anti-inflammatory.',
    client = { image = 'diclo.png' }
},
```

</details>

{% hint style="warning" %}
The images which we used to the items are in the **rd-pharmacyjob/images** folder
{% endhint %}

## SQL

<details>

<summary>UPLOAD THE SQL</summary>

```sql
CREATE TABLE IF NOT EXISTS `RD_PHARMACY` (
  `job_name` VARCHAR(50) NOT NULL,
  `balance` INT(11) NOT NULL DEFAULT 0,
  PRIMARY KEY (`job_name`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;
CREATE TABLE IF NOT EXISTS job_outfits (
    id INT AUTO_INCREMENT PRIMARY KEY,
    job VARCHAR(50) NOT NULL,
    grades LONGTEXT NOT NULL,
    name VARCHAR(100) NOT NULL,
    skin LONGTEXT NOT NULL
);
CREATE TABLE IF NOT EXISTS pharmacy_kicks (
    citizenid VARCHAR(50) NOT NULL,
    pharmacyName VARCHAR(50) NOT NULL,
    expires BIGINT NOT NULL,
    PRIMARY KEY(citizenid, pharmacyName)
);
CREATE TABLE IF NOT EXISTS `pharmacy_duty` (
    `id` int(11) NOT NULL AUTO_INCREMENT,
    `pharmacy` varchar(50) NOT NULL,
    `citizenid` varchar(50) NOT NULL,
    `minutes` int(11) NOT NULL DEFAULT 0,
    PRIMARY KEY (`id`),
    UNIQUE KEY `citizen_pharmacy` (`citizenid`, `pharmacy`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_general_ci;

```

</details>

### ASSET POSITION <a href="#asset-positioning" id="asset-positioning"></a>

{% hint style="danger" %}
Correctly position the assets in the server.cfg by following this step, if something goes wrong you will probably get errors about exports not found, do not skip this step!
{% endhint %}

```cfscript
ensure es_extended or qb-core or qbx-core

ensure ox_lib
ensure [inventory]

ensure rd-pharmacyjob
```

## SETUP THE SCRIPT WEBHOOK

{% hint style="warning" %}
**IF YOU WANT TO USE THE OPPORTUNITIES WHICH CAN BE GIVEN BY A WEBHOOK, THEN YOU WILL HAVE TO SET IT UP IN OUR ASSETS. YOU CAN DO THIS BY CHANGING A VALUE TO YOUR DISCORD WEBHOOK IN THE `WEBHOOK.LUA` FILE**
{% endhint %}

```lua
Settings = Settings or {}
Settings.Webhook = "YOUR_WEBHOOK_HERE"
```

{% content-ref url="../../guides/how-to-create-webhook.md" %}
[how-to-create-webhook.md](../../guides/how-to-create-webhook.md)
{% endcontent-ref %}
