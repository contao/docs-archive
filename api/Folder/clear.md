
Folder :: clear
-------------------------------------------

Empty the folder.


### Description ###

**Definition:** `public function clear()`

**Located in:** *system/libraries/Folder.php*

**Class hierarchy:** *[System](../System.md) > [Folder](../Folder.md)*


### Examples ###

1. Clear the temporary folder if not empty

	```php
	<?php

	$objFolder = new Folder('system/tmp');

	if (!$objFolder->isEmpty())
	{
		$objFolder->clear();
	}
	```


