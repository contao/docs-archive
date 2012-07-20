
Date :: __construct
-------------------------------------------

Create object properties and date ranges.


### Description ###

**Definition:** `public function __construct($intTstamp=false, $strFormat=false)`

**Located in:** *system/libraries/Date.php*

**Class hierarchy:** *[System](../System.md) > [Date](../Date.md)*


### Parameters ###

1. *integer* `$intTstamp`

	The timestamp to be converted.

2. *string* `$strFormat`

	The format according to PHP's [date()](http://php.net/manual/en/function.date.php) function.


### Examples ###

1. Convert the existing date to tstamp

	```php
	<?php

	$objDate = new Date('17-06-2012', 'd-m-Y');
	echo $objDate->tstamp;
	```
	> 1339891200

