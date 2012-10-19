
Database :: listTables
-------------------------------------------

Return all tables of a database as array.


### Description ###

**Definition:** `public function listTables($strDatabase=null, $blnNoCache=false)`

**Located in:** *system/libraries/Database.php*

**Class hierarchy:** *[Database](../Database.md)*


### Parameters ###

1. *string* `$strDatabase`

	Database name. If none provided, the default database will be used.

2. *boolean* `$blnNoCache`

	If true, no cache will be used. False by default.


### Return Values ###

Array of all tables in a certain database.


### Examples ###

1. Print the list of all Contao tables

	```php
	<?php

	print_r($this->Database->listTables());