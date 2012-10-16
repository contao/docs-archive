
Database :: getFieldNames
-------------------------------------------

Return the field names of a particular table as array.


### Description ###

**Definition:** `public function getFieldNames($strTable, $blnNoCache=false)`

**Located in:** *system/libraries/Database.php*

**Class hierarchy:** *[Database](../Database.md)*


### Parameters ###

1. *string* `$strTable`

	Table name.

2. *boolean* `$blnNoCache`

	If true, no cache will be used. False by default.


### Return Values ###

Array of names of all fields in a given table.


### Examples ###

1. Print the list of names of all fields in tl_news table

	```php
	<?php

	print_r($this->Database->getFieldNames('tl_news'));