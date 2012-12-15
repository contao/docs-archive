
File :: close
-------------------------------------------

Close the file handle.


### Description ###

**Definition:** `public function close()`

**Located in:** *system/libraries/File.php*

**Class hierarchy:** *[System](../System.md) > [File](../File.md)*


### Return Values ###

True on success, false otherwise.


### Examples ###

1. Close a file handle

	```php
	<?php

	$objFile = new File('tl_files/my_data.txt');
	$objFile->close();
	```


