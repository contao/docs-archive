
FTP :: copy
-------------------------------------------

Copy a file or folder.


### Description ###

**Definition:** `public function copy($strSource, $strDestination)`

**Located in:** *system/libraries/FTP.php*

**Class hierarchy:** *[Files](../Files.md) > [FTP](../FTP.md)*


### Parameters ###

1. *string* `$strSource`

	Path of the existing file.

2. *string* `$strDestination`

	Path of the new file.


### Return Values ###

True on success, false otherwise.


### Examples ###

1. Copy a file

	```php
	<?php

	$this->FTP->copy('tl_files/example_file.txt', 'tl_files/example_file_backup.txt');
	```


