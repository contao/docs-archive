
Files :: fputs
-------------------------------------------

Write content to a file.


### Description ###

**Definition:** `public function fputs($resFile, $strContent)`

**Located in:** *system/libraries/Files.php*

**Class hierarchy:** *[Files](../Files.md)*


### Parameters ###

1. *resource* `$resFile`

	A file handle.

2. *string* `$strContent`

	Content to be put into the file.


### Return Values ###

True on success, false otherwise.


### Examples ###

1. Put "Hello Contao!" text into a file

	```php
	<?php

	$resFile = $this->Files->fopen('tl_files/example_file.txt', 'w');
	$this->Files->fputs($resFile, 'Hello Contao!');
	```


