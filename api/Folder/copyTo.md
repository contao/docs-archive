
Folder :: copyTo
-------------------------------------------

Copy the folder.


### Description ###

**Definition:** `public function copyTo($strNewName)`

**Located in:** *system/libraries/Folder.php*

**Class hierarchy:** *[System](../System.md) > [Folder](../Folder.md)*


### Parameters ###

1. *string* `$strNewName`

	A relative path and name of the new folder.


### Return Values ###

True on success, false otherwise.


### Examples ###

1. Copy the folder

	```php
	<?php

	$objFolder = new Folder('tl_files/example_folder');
	$objFolder->copyTo('tl_files/example_folder_backup');
	```


