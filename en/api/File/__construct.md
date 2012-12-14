
File :: __construct
-------------------------------------------

Check whether a file exists.


### Description ###

**Definition:** `public function __construct($strFile)`

**Located in:** *system/libraries/File.php*

**Class hierarchy:** *[System](../System.md) > [File](../File.md)*


### Parameters ###

1. *string* `$strFile`

	A relative path of the file.


### Examples ###

1. Initialize a file object

	```php
	<?php

	$objFile = new File('tl_files/my_data.txt');
	```

