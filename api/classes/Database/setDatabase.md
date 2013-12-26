
Database :: setDatabase
-------------------------------------------

Change the current database.


### Description ###

**Definition:** `public function setDatabase($strDatabase)`

**Located in:** *system/libraries/Database.php*

**Class hierarchy:** *[Database](../Database.md)*


### Parameters ###

1. *string* `$strDatabase`

	Database name to be switched to.


### Return Values ###

True on success, false otherwise.


### Examples ###

1. Set the "test" database

	```php
	<?php

	$this->setDatabase('test');