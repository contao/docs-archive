
Config :: add
-------------------------------------------

Add a configuration variable to the local configuration file.


### Description ###

**Definition:** `public function add($strKey, $varValue)`

**Located in:** *system/libraries/Config.php*

**Class hierarchy:** *[Config](../Config.md)*


### Parameters ###

1. *string* `$strKey`

	Name of the configuration variable.

2. *mixed* `$varValue`

	Value of the configuration variable.



### Examples ###

1. Save the last update time

	```php
	<?php

	$this->Config->add('lastUpdate', $time);