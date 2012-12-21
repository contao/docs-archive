
Config :: getActiveModules
-------------------------------------------

Return all active modules (starting with "backend" and "frontend") as array.


### Description ###

**Definition:** `public function getActiveModules($blnNoCache=false)`

**Located in:** *system/libraries/Config.php*

**Class hierarchy:** *[Config](../Config.md)*


### Parameters ###

1. *boolean* `$blnNoCache`

	If set to true, no cache will be used.


### Return Values ###

Associative array of the active modules.


### Examples ###

1. Check if the comments module is active

	```php
	<?php

	if (in_array('comments', $this->Config->getActiveModules())
	{
		// Include comments
	}