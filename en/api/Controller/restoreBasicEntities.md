
Controller :: restoreBasicEntities
-------------------------------------------

Restore basic entities that were escaped by tinyMCE editor.


### Description ###

**Definition:** `protected function restoreBasicEntities($strBuffer)`

**Located in:** *system/libraries/Controller.php*

**Class hierarchy:** *[System](../System.php) > [Controller](../Controller.php)*


### Parameters ###

1. *string* `$strBuffer`

	A string to be parsed.


### Examples ###

1. Display a text with restored entities

	```php
	<?php

	$strText = 'The sky is[nbsp]blue today.';
	echo $this->restoreBasicEntities($strText);
	```
	> The sky is blue today.

