
File :: getContent
-------------------------------------------

Return file content as string.


### Description ###

**Definition:** `public function getContent()`

**Located in:** *system/libraries/File.php*

**Class hierarchy:** *[System](../System.md) > [File](../File.md)*


### Return Values ###

The file content as string.


### Examples ###

1. Get the file content

	```php
	<?php

	$objFile = new File('tl_files/my_data.txt');
	$strContent = $objFile->getContent();
	```


