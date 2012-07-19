
Controller :: getFrontendModule
-------------------------------------------

Generate a front end module and return it as HTML string.


### Description ###

**Definition:** `protected function getFrontendModule($intId, $strColumn='main')`

**Located in:** *system/libraries/Controller.php*

**Class hierarchy:** *[System](../System.php) > [Controller](../Controller.php)*


### Parameters ###

1. *integer* `$intId`

	The ID of the front end module.

2. *string* `$strColumn`

	The column which module is generated in.


### Return Values ###

The front end module as HTML string.


### Examples ###

1. Display the front end module with ID of 123

	```php
	<?php

	echo $this->getFrontendModule(123, $this->strColumn);
	```
	> ```<div class="mod_custom">just a test</div>```


### See Also ###

- [`Controller::getArticle`](getArticle.md) – Get an article front end module
- [`Controller::getContentElement`](getContentElement.md) – Get a content element
- [`Controller::getForm`](getForm.md) – Get a form