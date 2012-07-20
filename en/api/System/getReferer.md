
System :: getReferer
-------------------------------------------

Return the current referer URL and optionally encode ampersands.


### Description ###

**Definition:** `protected function getReferer($blnEncodeAmpersands=false, $strTable=null)`

**Located in:** *system/libraries/System*

**Class hierarchy:** *[System](../System.md)*


### Parameters ###

1. *boolean* `$blnEncodeAmpersands`

	If true, the ampersands will be encoded.

2. *string* `$strTable`

	The optional table name (used for back end only).


### Examples ###

1. Display the last page visited

	```php
	<?php

	echo $this->getReferer();
	```
	> calendar.html
