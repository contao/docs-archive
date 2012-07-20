
Controller :: getTimeZones
-------------------------------------------

Get all timezones and return them as array.


### Description ###

**Definition:** `protected function getTimeZones()`

**Located in:** *system/libraries/Controller.php*

**Class hierarchy:** *[System](../System.md) > [Controller](../Controller.md)*


### Return Values ###

An associative multidimensional array containing timezones grouped by sections.


### Examples ###

1. Display a list of all timezones

	```php
	<?php

	$arrTimezones = $this->getTimeZones();
	print_r($arrTimezones);
	```
	> Array ( [General] => Array ( [0] => CET [1] => CST6CDT [2] => EST [3] => EST5EDT ... ) ... )


### See Also ###

- [`Controller::getBackendLanguages`](getBackendLanguages.md) – Get backend languages
- [`Controller::getLanguages`](getLanguages.md) – Get all languages
- [`Controller::getCountries`](getCountries.md) – Get all countries