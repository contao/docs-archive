
Folder :: renameTo
-------------------------------------------

Rename the folder.


### Description ###

**Definition:** `public function renameTo($strNewName)`

**Located in:** *system/libraries/Folder.php*

**Class hierarchy:** *[System](../System.md) > [Folder](../Folder.md)*


### Parameters ###

1. *string* `$strName`

	A relative path and name of the new folder.


### Return Values ###

True on success, false otherwise.


### Examples ###

1. Rename the folder

	```php
	<?php

	$objFolder = new Folder('tl_files/old_folder');
	$objFolder->renameTo('tl_files/new_folder');
	echo $objFolder->value; // tl_files/new_folder
	```

