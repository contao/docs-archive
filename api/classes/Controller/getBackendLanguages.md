
Controller :: getBackendLanguages
-------------------------------------------

Return an array of supported back end languages.


### Description ###

**Definition:** `protected function getBackendLanguages()`

**Located in:** *system/libraries/Controller.php*

**Class hierarchy:** *[System](../System.md) > [Controller](../Controller.md)*


### Return Values ###

An associative array with available back end languages.


### Examples ###

1. Display a list of available back end languages

	```php
	<?php

	$arrLanguages = $this->getBackendLanguages();
	print_r($arrLanguages);
	```
	> Array ( [en] => English [de] => German - Deutsch )


### See also ###

- [`Controller::getLanguages`](getLanguages.md) – Get all languages
- [`Controller::getCountries`](getCountries.md) – Get all countries
- [`Controller::getTimeZones`](getTimeZones.md) – Get all time zones