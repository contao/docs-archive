
Folder :: isEmpty
-------------------------------------------

Return true if the folder is empty.


### Description ###

**Definition:** `public function isEmpty()`

**Located in:** *system/libraries/Folder.php*

**Class hierarchy:** *[System](../System.md) > [Folder](../Folder.md)*


### Return Values ###

True if folder is empty, false otherwise.


### Examples ###

1. Check if the folder is empty

	```php
	<?php

	$objFolder = new Folder('tl_files/example_folder');
	
	if ($objFolder->isEmpty())
	{
		// Create a new file
	}
	```


