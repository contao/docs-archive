
Controller :: getPageSections
-------------------------------------------

Return all page sections as array.


### Description ###

**Definition:** `protected function getPageSections()`

**Located in:** *system/libraries/Controller.php*

**Class hierarchy:** *[System](../System.php) > [Controller](../Controller.php)*


### Examples ###

1. Display all sections of the page

	```php
	<?php

	print_r($this->getPageSections());
	```
	> Array ( [0] => header [1] => left [2] => right [3] => main [4] => footer )
