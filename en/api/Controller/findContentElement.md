
Controller :: findContentElement
-------------------------------------------

Find a content element in the TL_CTE array and return its value.


### Description ###

**Definition:** `protected function findContentElement($strName)`

**Located in:** *system/libraries/Controller.php*

**Class hierarchy:** *[System](../System.php) > [Controller](../Controller.php)*


### Parameters ###

1. *string* `$strName`

	Name of the searched content element.


### Return Values ###

The class name of the content element, or an empty string if not found.
	

### Examples ###

1. Display the class name of gallery content element

	```php
	<?php

	echo $this->findContentElement('gallery');
	```
	> ContentGallery


### See Also ###

- [`Controller::findFrontendModule`](findFrontendModule.md) – Find a front end module


