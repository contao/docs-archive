
Controller :: replaceInsertTags
-------------------------------------------

Replace insert tags with their values.


### Description ###

**Definition:** `protected function replaceInsertTags($strBuffer, $blnCache=false)`

**Located in:** *system/libraries/Controller.php*

**Class hierarchy:** *[System](../System.php) > [Controller](../Controller.php)*


### Parameters ###

1. *string* `$strBuffer`

	A string to be parsed.

2. *boolean* `$blnCache`

	If set to true, the values of insert tags will not be cached.


### Return Values ###

A string with replaced insert tags with their actual values.


### Examples ###

1. Display a welcome message

	```php
	<?php

	$strText = 'Welcome to {{page::rootTitle}}!';
	echo $this->replaceInsertTags($strText);
	```
	> Welcome to Music Academy!

