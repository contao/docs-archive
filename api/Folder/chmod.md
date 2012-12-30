
Folder :: chmod
-------------------------------------------

Set the folder permissions.


### Description ###

**Definition:** `public function chmod($strChmod)`

**Located in:** *system/libraries/Folder.php*

**Class hierarchy:** *[System](../System.md) > [Folder](../Folder.md)*


### Parameters ###

1. *string* `$strChmod`

	The CHMOD value to be set. Make sure you include the *0* before value, e.g. 0644.


### Return Values ###

True on success, false otherwise.


### Examples ###

1. Make folder writeable

	```php
	<?php

	$objFolder = new Folder('tl_files/example_folder');
	$objFolder->chmod(0644);
	```


