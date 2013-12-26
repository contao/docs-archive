
File :: getContentAsArray
-------------------------------------------

Return file content as array.


### Description ###

**Definition:** `public function getContentAsArray()`

**Located in:** *system/libraries/File.php*

**Class hierarchy:** *[System](../System.md) > [File](../File.md)*


### Return Values ###

The file content as array.


### Examples ###

1. Get the file content

	```php
	<?php

	$objFile = new File('tl_files/my_data.txt');
	$arrContent = $objFile->getContentAsArray();
	```


