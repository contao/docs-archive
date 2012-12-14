
File :: truncate
-------------------------------------------

Truncate the file.


### Description ###

**Definition:** `public function truncate()`

**Located in:** *system/libraries/File.php*

**Class hierarchy:** *[System](../System.md) > [File](../File.md)*


### Return Values ###

True on success, false otherwise.


### Examples ###

1. Truncate a file

	```php
	<?php

	$objFile = new File('tl_files/my_data.txt');
	$objFile->truncate();
	```


