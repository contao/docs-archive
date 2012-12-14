
File :: chmod
-------------------------------------------

Set the file permissions.


### Description ###

**Definition:** `public function chmod($strChmod)`

**Located in:** *system/libraries/File.php*

**Class hierarchy:** *[System](../System.md) > [File](../File.md)*


### Parameters ###

1. *string* `$strChmod`

	The CHMOD value to be set.


### Return Values ###

True on success, false otherwise.


### Examples ###

1. Set the write permissions

	```php
	<?php

	$objFile = new File('tl_files/my_data.txt');
	$objFile->chmod(644);
	```


