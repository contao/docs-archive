
Controller :: findFrontendModule
-------------------------------------------

Find a front end module in the FE_MOD array and return its value.


### Description ###

**Definition:** `protected function findFrontendModule($strName)`

**Located in:** *system/libraries/Controller.php*

**Class hierarchy:** *[System](../System.php) > [Controller](../Controller.php)*


### Parameters ###

1. *string* `$strName`

	Name of the searched front end module.
	

### Examples ###

1. Display the class name of news list front end module

	```php
	<?php

	echo $this->findFrontendModule('newslist');
	```
	> ModuleNewsList


