
Date :: formatJs
-------------------------------------------

Convert a PHP format string into a JavaScript format string.


### Description ###

**Definition:** `public static function formatToJs($strFormat)`

**Located in:** *system/libraries/Date.php*

**Class hierarchy:** *[System](../System.md) > [Date](../Date.md)*

**Throws:** *Exception*


### Parameters ###

1. *string* `$strFormat`

	The date format to be converted.


### Return Values ###

A valid JavaScript date format.


### Examples ###

1. Convert the existing date to tstamp

	```php
	<?php

	echo Date::formatToJs('d-m-Y');
	```
	> %d-%m-%Y


### See Also ###

- [`Date::getInputFormat`](getInputFormat.md) – Return an input format string for a particular date