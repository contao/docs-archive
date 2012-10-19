
Database :: listFields
-------------------------------------------

Return all columns of a particular table as array.


### Description ###

**Definition:** `public function listFields($strTable, $blnNoCache=false)`

**Located in:** *system/libraries/Database.php*

**Class hierarchy:** *[Database](../Database.md)*


### Parameters ###

1. *string* `$strTable`

	Table name.

2. *boolean* `$blnNoCache`

	If true, no cache will be used. False by default.


### Return Values ###

Array of all fields in a given table.


### Examples ###

1. Print the list of all fields in tl_news

	```php
	<?php

	print_r($this->Database->listFields('tl_news'));