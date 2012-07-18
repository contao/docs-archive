
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


### Examples ###

1. Display a list of all available languages

	```php
	<?php

	$arrLanguages = $this->getLanguages();
	print_r($arrLanguages);
	```
	> Array ( [om] => (Afan) Oromo [ab] => Abkhazian [aa] => Afar [af] => Afrikaans ... )
