
File :: delete
-------------------------------------------

Delete the file.


### Description ###

**Definition:** `public function delete()`

**Located in:** *system/libraries/File.php*

**Class hierarchy:** *[System](../System.md) > [File](../File.md)*


### Return Values ###

True on success, false otherwise.


### Examples ###

1. Delete a file

	```php
	<?php

	$objFile = new File('tl_files/my_data.txt');
	$objFile->delete();
	```


