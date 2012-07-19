
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


### Return Values ###

The class name of the front end module, or an empty string if not found.
	

### Examples ###

1. Display the class name of news list front end module

	```php
	<?php

	echo $this->findFrontendModule('newslist');
	```
	> ModuleNewsList


### See Also ###

- [`Controller::findContentElement`](findContentElement.md) – Find a content element
