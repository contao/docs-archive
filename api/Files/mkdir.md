
Files :: mkdir
-------------------------------------------

Create a directory.


### Description ###

**Definition:** `public function mkdir($strDirectory)`

**Located in:** *system/libraries/Files.php*

**Class hierarchy:** *[Files](../Files.md)*


### Parameters ###

1. *string* `$strDirectory`

	Path of directory to be created.


### Return Values ###

True on success, false otherwise.


### Examples ###

1. Create a directory

	```php
	<?php

	$this->Files->mkdir('tl_files/example_folder');
	```


