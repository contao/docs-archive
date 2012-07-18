
Controller :: parseSimpleTokens
-------------------------------------------

Parse simple tokens that can be used to e.g. personalize newsletters.


### Description ###

**Definition:** `protected function parseSimpleTokens($strBuffer, $arrData)`

**Located in:** *system/libraries/Controller.php*

**Class hierarchy:** *[System](../System.php) > [Controller](../Controller.php)*


### Parameters ###

1. *string* `$strBuffer`

	A string to be parsed.

2. *array* `$arrData`

	The associative array with replacement values.


### Examples ###

1. Display a personalized welcome message

	```php
	<?php

	$arrData = array
	(
		'firstname' => 'John',
		'lastname' => 'Doe'
	);

	echo $this->parseSimpleTokens('Hello ##firstname## ##lastname##!', $arrData);
	```
	> Hello John Doe!

