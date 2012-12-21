
System :: getFormattedNumber
-------------------------------------------

Format a number.


### Description ###

**Definition:** `protected function getFormattedNumber($varNumber, $intDecimals=2)`

**Located in:** *system/libraries/System*

**Class hierarchy:** *[System](../System.md)*


### Parameters ###

1. *mixed* `$varNumber`

	The number that should be formatted.

2. *integer* `$intDecimals`

	The number of decimals.


### Return Values ###

The formatted number according to provided settings and language (decimal and thousands separator).
	

### Examples ###

1. Display the formatted number

	```php
	<?php

	echo $this->getFormattedNumber(1234567);
	```
	> 1,234,567.00

