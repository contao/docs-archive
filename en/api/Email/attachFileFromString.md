
Email :: attachFileFromString
-------------------------------------------

Attach a file from a string.


### Description ###

**Definition:** `public function attachFileFromString($strContent, $strFilename, $strMime='application/octet-stream')`

**Located in:** *system/libraries/Email*

**Class hierarchy:** *[System](../System.php) > [Email](../Email)*


### Parameters ###

1. *string* `$strContent`

	The file content.
		

2. *string* `$strFilename`

	The name of the file.
		

3. *string* `$strMime`

	The MIME type of the file.


### Examples ###

1. Attach a file to the e-mail

	```php
	<?php

	$strFile = file_get_contents(TL_ROOT . '/tl_files/files/example.txt');
	$objEmail = new Email();
	$objEmail->attachFileFromString($strFile, 'example.txt');
	```
	

### See Also ###

- [`Email::attachFile`](attachFile.md) – Attach the file
