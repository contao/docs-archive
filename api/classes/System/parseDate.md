
System :: parseDate
-------------------------------------------

Parse a date format string and translate textual representations.


### Description ###

**Definition:** `protected function parseDate($strFormat, $intTstamp=null)`

**Located in:** *system/libraries/System*

**Class hierarchy:** *[System](../System.md)*


### Parameters ###

1. *string* `$strFormat`

	The date form according to PHP's [date()](http://php.net/manual/en/function.date.php) function.

1. *integer* `$intTstamp`

	An optional timestamp. If none provided, the current time will be used.


### Return Values ###

The formatted date and/or time.


### Examples ###

1. Display the current date and time

	```php
	<?php

	echo $this->parseDate($GLOBALS['TL_CONFIG']['datimFormat']);
	```
	> 2012-07-20 18:32

