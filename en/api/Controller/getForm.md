
Controller :: getForm
-------------------------------------------

Generate a form with specified ID or alias and return it as HTML string.


### Description ###

**Definition:** `protected function getForm($varId)`

**Located in:** *system/libraries/Controller.php*

**Class hierarchy:** *[System](../System.php) > [Controller](../Controller.php)*


### Parameters ###

1. *mixed* `$varId`

	The numberic ID or alias of the form.


### Return Values ###

The form as HTML string.


### Examples ###

1. Display the form with the ID of 123

	```php
	<?php

	echo $this->getForm(123);
	```

