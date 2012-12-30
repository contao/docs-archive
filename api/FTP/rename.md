
FTP :: rename
-------------------------------------------

Rename a file or folder.


### Description ###

**Definition:** `public function rename($strOldName, $strNewName)`

**Located in:** *system/libraries/FTP.php*

**Class hierarchy:** *[Files](../Files.md) > [FTP](../FTP.md)*


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

	$this->FTP->rename('tl_files/old_file.txt', 'tl_files/new_file.txt');
	```


