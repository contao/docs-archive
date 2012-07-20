
System :: splitFriendlyName
-------------------------------------------

Split a friendly name address and return name and e-mail as array.


### Description ###

**Definition:** `protected function splitFriendlyName($strEmail)`

**Located in:** *system/libraries/System*

**Class hierarchy:** *[System](../System.md)*


### Parameters ###

1. *string* `$strEmail`

	The e-mail address to be parsed.


### Return Values ###

An array containing a name and an e-mail address.


### Examples ###

1. Split the friendly e-mail address

	```php
	<?php

	print_r($this->splitFriendlyName('Admin <admin@example.com>'));
	```
	> Array ( [0] => Admin [1] => admin@example.com )

