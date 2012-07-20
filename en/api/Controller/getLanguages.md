
Controller :: getLanguages
-------------------------------------------

Return all languages as array.


### Description ###

**Definition:** `protected function getLanguages($blnBeOnly=false)`

**Located in:** *system/libraries/Controller.php*

**Class hierarchy:** *[System](../System.php) > [Controller](../Controller.php)*



### Parameters ###

1. *boolean* `$blnBeOnly`

	Return only the languages of back end.


### Return Values ###

An associative array of the available languages. If ```$blnBeOnly``` is set to true, it will return an associative array of the available back end languages.


### Examples ###

1. Display a list of all available languages

	```php
	<?php

	$arrLanguages = $this->getLanguages();
	print_r($arrLanguages);
	```
	> Array ( [om] => (Afan) Oromo [ab] => Abkhazian [aa] => Afar [af] => Afrikaans ... )


### See Also ###

- [`Controller::getBackendLanguages`](getBackendLanguages.md) – Get backend languages
- [`Controller::getCountries`](getCountries.md) – Get all countries
- [`Controller::getTimeZones`](getTimeZones.md) – Get all time zones