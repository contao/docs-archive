
Input :: setGet
-------------------------------------------

Set a $_GET parameter.


### Description ###

**Definition:** `public function setGet($strKey, $varValue)`

**Located in:** *system/libraries/Input.php*

**Class hierarchy:** *[Input](../Input.md)*


### Parameters ###

1. *string* `$strKey`

	Name of the $_GET property to be set.

2. *mixed* `$varValue`

	Value of the $_GET property to be set.


### Examples ###

1. Set a page parameter to 3

	```php
	<?php

	$this->Input->setGet('page', 3);
	```


### See Also ###

- [`Input::get`](get.md) – Return a $_GET parameter

