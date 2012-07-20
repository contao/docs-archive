
Email :: attachFile
-------------------------------------------

Attach a file.


### Description ###

**Definition:** `public function attachFile($strFile, $strMime='application/octet-stream')`

**Located in:** *system/libraries/Email*

**Class hierarchy:** *[System](../System.php) > [Email](../Email)*


### Parameters ###

1. *string* `$strFile`

	A full path to the file.
		

2. *string* `$strMime`

	The MIME type of the file.


### Examples ###

1. Attach a file to the e-mail

	```php
	<?php

	$objEmail = new Email();
	$objEmail->attachFile(TL_ROOT . '/tl_files/files/example.txt');
	

### See Also ###

- [`Controller::attachFileFromString`](attachFileFromString.md) – Attach the file from a string
