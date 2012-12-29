
Files :: rename
-------------------------------------------

Rename a file or folder.


### Description ###

**Definition:** `public function rename($strOldName, $strNewName)`

**Located in:** *system/libraries/Files.php*

**Class hierarchy:** *[Files](../Files.md)*


### Parameters ###

1. *string* `$strOldName`

	Path of the existing file.

2. *string* `$strNewName`

	Path of the new file.


### Return Values ###

True on success, false otherwise.


### Examples ###

1. Rename a file

	```php
	<?php

	$this->Files->rename('tl_files/old_file.txt', 'tl_files/new_file.txt');
	```


