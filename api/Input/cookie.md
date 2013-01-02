
Input :: cookie
-------------------------------------------

Return a $_COOKIE parameter


### Description ###

**Definition:** `public function cookie($strKey, $blnDecodeEntities=false)`

**Located in:** *system/libraries/Input.php*

**Class hierarchy:** *[Input](../Input.md)*


### Parameters ###

1. *string* `$strKey`

	Name of the $_COOKIE parameter to be returned.

2. *boolean* `$blnDecodeEntities`

	If true, the entities will be decoded. Defaults to false.


### Return Values ###

Mixed values.


### Examples ###

1. Get the last visit time

	```php
	<?php

	$lastVisit = $this->Input->cookie('LAST_VISIT');
	```


### See Also ###

- [`Input::setCookie`](setCookie.md) – Set a $_COOKIE parameter


