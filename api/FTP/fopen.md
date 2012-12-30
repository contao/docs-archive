
FTP :: fopen
-------------------------------------------

Open a file and return the handle.


### Description ###

**Definition:** `public function fopen($strFile, $strMode)`

**Located in:** *system/libraries/FTP.php*

**Class hierarchy:** *[Files](../Files.md) > [FTP](../FTP.md)*


### Parameters ###

1. *string* `$strFile`

	Path of file to be opened.

2. *string* `$strMode`

	Mode the file will be opened in. For the full list please refer to http://php.net/manual/function.fopen.php.


### Return Values ###

A file handle.


### Examples ###

1. Open a file for reading only

	```php
	<?php

	$resFile = $this->FTP->fopen('tl_files/example_file.txt', 'r');
	```


