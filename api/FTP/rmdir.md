
FTP :: rmdir
-------------------------------------------

Remove a directory.


### Description ###

**Definition:** `public function rmdir($strDirectory)`

**Located in:** *system/libraries/FTP.php*

**Class hierarchy:** *[Files](../Files.md) > [FTP](../FTP.md)*


### Parameters ###

1. *string* `$strDirectory`

	Path of directory to be removed.


### Return Values ###

True on success, false otherwise.


### Examples ###

1. Delete a directory

	```php
	<?php

	$this->FTP->rmdir('tl_files/example_folder');
	```


