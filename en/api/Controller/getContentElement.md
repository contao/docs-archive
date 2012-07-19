
Controller :: getContentElement
-------------------------------------------

Generate a content element with specified ID and return it as HTML string.


### Description ###

**Definition:** `protected function getContentElement($intId)`

**Located in:** *system/libraries/Controller.php*

**Class hierarchy:** *[System](../System.php) > [Controller](../Controller.php)*


### Parameters ###

1. *integer* `$intId`

	The numberic ID of the content element.


### Return Values ###

The content element as HTML string.


### Examples ###

1. Display the content element with the ID of 123

	```php
	<?php

	echo $this->getContentElement(123);
	```

