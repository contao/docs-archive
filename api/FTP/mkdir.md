
FTP :: mkdir
-------------------------------------------

Create a directory.


### Description ###

**Definition:** `public function mkdir($strDirectory)`

**Located in:** *system/libraries/FTP.php*

**Class hierarchy:** *[Files](../Files.md) > [FTP](../FTP.md)*


### Parameters ###

1. *string* `$strDirectory`

	Path of directory to be created.


### Return Values ###

True on success, false otherwise.


### Examples ###

1. Create a directory

	```php
	<?php

	$this->FTP->mkdir('tl_files/example_folder');
	```


