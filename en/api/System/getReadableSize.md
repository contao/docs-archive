
System :: getReadableSize
-------------------------------------------

Convert a filesize into a human readable format.


### Description ###

**Definition:** `protected function getReadableSize($intSize, $intDecimals=1)`

**Located in:** *system/libraries/System*

**Class hierarchy:** *[System](../System.md)*


### Parameters ###

1. *integer* `$intSize`

	The file size in bytes.

2. *integer* `$intDecimals`

	The number of decimals.


### Return Values ###

The file size in human format.
	

### Examples ###

1. Get a file size of the screenshot

	```php
	<?php

	$strFile = TL_ROOT . '/tl_files/music_academy/screenshot.jpg';
	echo $this->getReadableSize(filesize($strFile));
	```
	> 21.8 kB

