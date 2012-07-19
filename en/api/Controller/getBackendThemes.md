
Controller :: getBackendThemes
-------------------------------------------

Get all back end themes and return them as array.


### Description ###

**Definition:** `protected function getBackendThemes()`

**Located in:** *system/libraries/Controller.php*

**Class hierarchy:** *[System](../System.php) > [Controller](../Controller.php)*


### Return Values ###

An associative array with available back end themes.


### Examples ###

1. Display a list of back end themes

	```php
	<?php

	$arrThemes = $this->getBackendThemes();
	print_r($arrThemes);
	```
	> Array ( [default] => default )
