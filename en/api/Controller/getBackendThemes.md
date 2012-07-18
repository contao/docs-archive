
Controller :: getBackendThemes
-------------------------------------------

Get all back end themes and return them as array.


### Description ###

**Definition:** `protected function getBackendThemes()`

**Located in:** *system/libraries/Controller.php*

**Class hierarchy:** *[System](../System.php) > [Controller](../Controller.php)*


### Examples ###

1. Display a list of back end themes

	```php
	<?php

	$arrThemes = $this->getBackendThemes();
	print_r($arrThemes);
	```
	> Array ( [default] => default )
