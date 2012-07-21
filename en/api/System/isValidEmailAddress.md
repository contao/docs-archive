
System :: isValidEmailAddress
-------------------------------------------

Validate an e-mail address.


### Description ###

**Definition:** `protected function isValidEmailAddress($strEmail)`

**Located in:** *system/libraries/System*

**Class hierarchy:** *[System](../System.md)*


### Parameters ###

1. *string* `$strEmail`

	The e-mail address to be validated.


### Return Values ###

True if the e-mail address is valid, false otherwise
	

### Examples ###

1. Check if the e-mail address is valid

	```php
	<?php

	if ($this->isValidEmailAddress('admin@example.com')
	{
		echo 'This is a valid e-mail address!';
	}
	```
	> This is a valid e-mail address!

