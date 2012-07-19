
Controller :: getCountries
-------------------------------------------

Get all countries and return them as array.


### Description ###

**Definition:** `protected function getCountries()`

**Located in:** *system/libraries/Controller.php*

**Class hierarchy:** *[System](../System.php) > [Controller](../Controller.php)*


### Return Values ###

An associative array of all available countries.


### Examples ###

1. Display a list of all countries

	```php
	<?php

	$arrCountries = $this->getCountries();
	print_r($arrCountries);
	```
	> Array ( [af] => Afghanistan [ax] => Aland Islands [al] => Albania [dz] => Algeria ... )
