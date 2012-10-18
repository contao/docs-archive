
Database :: tableExists
-------------------------------------------

Determine if a particular database table exists.


### Description ###

**Definition:** `public function tableExists($strTable, $strDatabase=null, $blnNoCache=false)`

**Located in:** *system/libraries/Database.php*

**Class hierarchy:** *[Database](../Database.md)*


### Parameters ###

1. *string* `$strTable`

	Table name.

2. *string* `$strDatabase`

	Database name. If none provided, the default database will be used.

3. *boolean* `$blnNoCache`

	If true, no cache will be used. False by default.


### Return Values ###

True if the table exists, false otherwise.


### Examples ###

1. Check if the table tl_custom exists

	```php
	<?php

	if ($this->Database->tableExists('tl_custom'))
	{
		echo 'Table tl_custom exists!';
	}