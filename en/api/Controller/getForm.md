
Controller :: getForm
-------------------------------------------

Generate a form with specified ID or alias and return it as HTML string.


### Description ###

**Definition:** `protected function getForm($varId)`

**Located in:** *system/libraries/Controller.php*

**Class hierarchy:** *[System](../System.md) > [Controller](../Controller.md)*


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


### See Also ###

- [`Controller::getArticle`](getArticle.md) – Get an article front end module
- [`Controller::getContentElement`](getContentElement.md) – Get a content element
- [`Controller::getFrontendModule`](getFrontendModule.md) – Get a front end module

