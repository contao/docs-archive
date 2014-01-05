
Database :: fieldExists
-------------------------------------------

Determine if a particular column exists.


### Description ###

**Definition:** `public function fieldExists($strField, $strTable, $blnNoCache=false)`

**Located in:** *system/libraries/Database.php*

**Class hierarchy:** *[Database](../Database.md)*


### Parameters ###

1. *string* `$strField`

	Field name to be checked.

2. *string* `$strTable`

	Table name.

3. *boolean* `$blnNoCache`

	If true, no cache will be used. False by default.


### Return Values ###

True if the field exists, false otherwise.


### Examples ###

1. Check if the field "author" table tl_news exists

	```php
	<?php

	if ($this->Database->fieldExists('author', 'tl_news'))
	{
		echo 'Field "author" exists in tl_news table!';
	}