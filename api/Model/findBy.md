
Model :: findBy
-------------------------------------------

Find a record by its reference field and return true if it has been found.


### Description ###

**Definition:** `public function findBy($strRefField, $varRefId)`

**Located in:** *system/libraries/Model.php*

**Class hierarchy:** *[System](../System.md) > [Model](../Model.md)*


### Parameters ###

1. *string* `$strRefField`

	A reference field name.

2. *mixed* `$varRefId`

	A reference field value.


### Return Values ###

True if the record is found, false otherwise.


### Examples ###

1. Try to find a record and display it

	```php
	<?php

	if ($objModel->findBy('id', 123))
	{
		// Display model data
	}
	```