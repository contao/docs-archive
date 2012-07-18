
Controller :: getTimeZones
-------------------------------------------

Get all timezones and return them as array.


### Description ###

**Definition:** `protected function getTimeZones()`

**Located in:** *system/libraries/Controller.php*

**Class hierarchy:** *[System](../System.php) > [Controller](../Controller.php)*


### Examples ###

1. Display a list of all timezones

	```php
	<?php

	$arrTimezones = $this->getTimeZones();
	print_r($arrTimezones);
	```
	> Array ( [General] => Array ( [0] => CET [1] => CST6CDT [2] => EST [3] => EST5EDT ... ) ... )
