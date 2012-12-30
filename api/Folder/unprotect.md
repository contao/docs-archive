
Folder :: unprotect
-------------------------------------------

Unprotect the folder by removing the .htaccess file.


### Description ###

**Definition:** `public function unprotect()`

**Located in:** *system/libraries/Folder.php*

**Class hierarchy:** *[System](../System.md) > [Folder](../Folder.md)*


### Examples ###

1. Unprotect the folder

	```php
	<?php

	$objFolder = new Folder('tl_files/example_folder');
	$objFolder->unprotect();
	```


