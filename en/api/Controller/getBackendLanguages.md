
Controller :: getBackendLanguages
-------------------------------------------

Return an array of supported back end languages.


### Description ###

**Definition:** `protected function getBackendLanguages()`

**Located in:** *system/libraries/Controller.php*

**Class hierarchy:** *[System](../System.php) > [Controller](../Controller.php)*


### Examples ###

1. Display a list of available back end languages

	```php
	<?php

	$arrLanguages = $this->getBackendLanguages();
	print_r($arrLanguages);
	```
	> Array ( [en] => English [de] => German - Deutsch )
