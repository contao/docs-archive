
Files :: rmdir
-------------------------------------------

Remove a directory.


### Description ###

**Definition:** `public function rmdir($strDirectory)`

**Located in:** *system/libraries/Files.php*

**Class hierarchy:** *[Files](../Files.md)*


### Parameters ###

1. *string* `$strDirectory`

	Path of directory to be removed.


### Return Values ###

True on success, false otherwise.


### Examples ###

1. Delete a directory

	```php
	<?php

	$this->Files->rmdir('tl_files/example_folder');
	```


