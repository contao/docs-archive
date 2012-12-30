
FTP :: is_writeable
-------------------------------------------

Check whether a file is writeable.


### Description ###

**Definition:** `public function is_writeable($strFile)`

**Located in:** *system/libraries/FTP.php*

**Class hierarchy:** *[Files](../Files.md) > [FTP](../FTP.md)*


### Parameters ###

1. *string* `$strFile`

	Path of the file to be checked.


### Return Values ###

True if the file is writeable, false otherwise.


### Examples ###

1. Check if the file is writeable

	```php
	<?php

	if (!$this->FTP->is_writeable('tl_files/example_file.txt'))
	{
		$this->FTP->chmod('tl_files/example_file.txt', 644);
	}
	```


