
Input :: get
-------------------------------------------

Return a $_GET parameter.


### Description ###

**Definition:** `public function get($strKey, $blnDecodeEntities=false)`

**Located in:** *system/libraries/Input.php*

**Class hierarchy:** *[Input](../Input.md)*


### Parameters ###

1. *string* `$strKey`

	Name of the $_GET parameter to be returned.

2. *boolean* `$blnDecodeEntities`

	If true, the entities will be decoded. Defaults to false.


### Return Values ###

Mixed values.


### Examples ###

1. Get the current page number (pagination)

	```php
	<?php

	$page = $this->Input->get('page');
	```


### See Also ###

- [`Input::setGet`](setGet.md) – Set a $_GET parameter

