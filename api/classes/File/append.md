
File :: append
-------------------------------------------

Append data to the file.


### Description ###

**Definition:** `public function append($varData, $strLine="\n")`

**Located in:** *system/libraries/File.php*

**Class hierarchy:** *[System](../System.md) > [File](../File.md)*


### Parameters ###

1. *mixed* `$varData`

	Data to be appended to the file.

2. *mixed* `$strLine`

	The line ending character.


### Return Values ###

True on success, false otherwise.


### Examples ###

1. Append data to the file

	```php
	<?php

	$objFile = new File('tl_files/my_data.txt');
	$objFile->append('Hello World!');
	```


