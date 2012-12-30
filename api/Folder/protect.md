
Folder :: protect
-------------------------------------------

Protect the folder by adding an .htaccess file.


### Description ###

**Definition:** `public function protect()`

**Located in:** *system/libraries/Folder.php*

**Class hierarchy:** *[System](../System.md) > [Folder](../Folder.md)*


### Examples ###

1. Protect the folder

	```php
	<?php

	$objFolder = new Folder('tl_files/confidental_data');
	$objFolder->protect();
	```


