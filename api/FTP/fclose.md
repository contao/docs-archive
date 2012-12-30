
FTP :: fclose
-------------------------------------------

Close a file.


### Description ###

**Definition:** `public function fclose($resFile)`

**Located in:** *system/libraries/FTP.php*

**Class hierarchy:** *[Files](../Files.md) > [FTP](../FTP.md)*


### Parameters ###

1. *resource* `$resFile`

	A file handle.


### Return Values ###

True on success, false otherwise.


### Examples ###

1. Write "Hello Contao!" text to a file and close it

	```php
	<?php

	$resFile = $this->FTP->fopen('tl_files/example_file.txt', 'w');
	$this->FTP->fputs($resFile, 'Hello Contao!');
	$this->FTP->fclose($resFile);
	```


