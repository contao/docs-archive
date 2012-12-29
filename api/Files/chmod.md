
Files :: chmod
-------------------------------------------

Chane file mode.


### Description ###

**Definition:** `public function chmod($strFile, $varMode)`

**Located in:** *system/libraries/Files.php*

**Class hierarchy:** *Files*


### Parameters ###

1. *string* `$strFile`

	Path of the file to be affected.

2. *mixed* `$varMode`

	The file mode to be used.


### Return Values ###

True on success, false otherwise.


### Examples ###

1. Make a file writeable

	```php
	<?php

	$this->Files->chmod('tl_files/example_file.txt', 644);
	```


