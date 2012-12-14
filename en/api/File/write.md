
File :: write
-------------------------------------------

Write data to the file.


### Description ###

**Definition:** `public function write($varData)`

**Located in:** *system/libraries/File.php*

**Class hierarchy:** *[System](../System.md) > [File](../File.md)*


### Parameters ###

1. *mixed* `$varData`

	Data to be written to the file.


### Return Values ###

True on success, false otherwise.


### Examples ###

1. Write data to the file

	```php
	<?php

	$objFile = new File('tl_files/my_data.txt');
	$objFile->write('Hello World!');
	```


