
System :: loadLanguageFile
-------------------------------------------

Load a set of language files.


### Description ###

**Definition:** `protected function loadLanguageFile($strName, $strLanguage=false, $blnNoCache=false)`

**Located in:** *system/libraries/System*

**Class hierarchy:** *[System](../System.md)*


### Parameters ###

1. *string* `$strName`

	Name of the language files (e.g. *countries* to access ```$GLOBALS['TL_LANG']['CNT']```).

2. *string* `$strLanguage`

	An optional language key. If none provided, the current one will be used.

3. *boolean* `$blnNoCache`

	If set to true, the cache will not be used.


### Examples ###

1. Load the countries language files

	```php
	<?php

	$this->loadLanguageFile('countries');
	echo $GLOBALS['TL_LANG']['CNT']['pl'];
	```
	> Poland

