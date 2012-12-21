
System :: import
-------------------------------------------

Import a library and make it accessible by its name or an optional key.


### Description ###

**Definition:** `protected function import($strClass, $strKey=null, $blnForce=false)`

**Located in:** *system/libraries/System*

**Class hierarchy:** *[System](../System.md)*


### Parameters ###

1. *string* `$strClass`

	The class name.

2. *string* `$strKey`

	The optional key to be used as alias.

3. *boolean* `$blnForce`

	If set to true, the library will be imported even if it already exists.


### Examples ###

1. Import the front end user object

	```php
	<?php

	$this->import('FrontendUser', 'User');
	echo $this->User->firstname;
	```
	> John

