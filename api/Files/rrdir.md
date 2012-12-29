
Files :: rrdir
-------------------------------------------

Recursively remove a directory.


### Description ###

**Definition:** `public function rrdir($strFolder, $blnPreserveRoot=false)`

**Located in:** *system/libraries/Files.php*

**Class hierarchy:** *[Files](../Files.md)*


### Parameters ###

1. *string* `$string`

	Path of directory to be recursively remoted.

2. *boolean* `$blnPreserveRoot`

	If set to true, it will preserve the root directory. In other words, it will simply empty a folder. Defaults to false.


### Examples ###

1. Empty a directory

	```php
	<?php

	$this->Files->rrdir('tl_files/example_folder', true);
	```


