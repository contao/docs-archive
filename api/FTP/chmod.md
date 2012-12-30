
FTP :: chmod
-------------------------------------------

Chane file mode.


### Description ###

**Definition:** `public function chmod($strFile, $varMode)`

**Located in:** *system/libraries/FTP.php*

**Class hierarchy:** *[Files](../Files.md) > [FTP](../FTP.md)*


### Parameters ###

1. *string* `$strFile`

	Path of the file to be affected.

2. *mixed* `$varMode`

	The CHMOD value to be set. Make sure you include the *0* before value, e.g. 0644


### Return Values ###

True on success, false otherwise.


### Examples ###

1. Make a file writeable

	```php
	<?php

	$this->FTP->chmod('tl_files/example_file.txt', 0644);
	```


