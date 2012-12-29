
Files :: delete
-------------------------------------------

Delete a file.


### Description ###

**Definition:** `public function delete($strFile)`

**Located in:** *system/libraries/Files.php*

**Class hierarchy:** *[Files](../Files.md)*


### Parameters ###

1. *string* `$strFile`

	Path of file to be deleted.


### Return Values ###

True on success, false otherwise.


### Examples ###

1. Delete a file

	```php
	<?php

	$this->Files->delete('tl_files/example_file.txt');
	```


