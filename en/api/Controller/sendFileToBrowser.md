
Controller :: sendFileToBrowser
-------------------------------------------

Send a file to the browser so the "save as" dialogue opens.


### Description ###

**Definition:** `protected function sendFileToBrowser($strFile)`

**Located in:** *system/libraries/Controller.php*

**Class hierarchy:** *[System](../System.md) > [Controller](../Controller.md)*


### Parameters ###

1. *string* `$strFile`

	A relative path to the file that will be send.


### Examples ###

1. Download the file if it is requested

	```php
	<?php

	if ($this->Input->get('file', true) != '')
	{
		$this->sendFileToBrowser($this->Input->get('file', true));
	}
	```

