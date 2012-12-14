
File :: copyTo
-------------------------------------------

Copy the file.


### Description ###

**Definition:** `public function copyTo($strNewName)`

**Located in:** *system/libraries/File.php*

**Class hierarchy:** *[System](../System.md) > [File](../File.md)*


### Parameters ###

1. *string* `$strName`

	A relative path and name of the new file.


### Return Values ###

True on success, false otherwise.


### Examples ###

1. Rename the file

	```php
	<?php

	$objFile = new File('tl_files/my_data.txt');
	$objFile->copy('tl_files/my_data_backup.txt');
	```


