
Controller :: classFileExists
-------------------------------------------

Return true if a class file exists.


### Description ###

**Definition:** `protected function classFileExists($strClass, $blnNoCache=false)`

**Located in:** *system/libraries/Controller.php*

**Class hierarchy:** *[System](../System.md) > [Controller](../Controller.md)*


### Parameters ###

1. *string* `$strClass`

	The class name.

2. *boolean* `$blnNoCache`

	If set to true, the cache will not be used.


### Return Values ###

True if the class file exists, false otherwise.


### Examples ###

1. Check if Comments module is installed

	```php
	<?php

	if ($this->classFileExists('Comments'))
	{
		echo 'Comments functionality available.';
	}
	```

