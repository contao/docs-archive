
Database :: lockTables
-------------------------------------------

Lock one or more tables.


### Description ###

**Definition:** `public function lockTables($arrTables)`

**Located in:** *system/libraries/Database.php*

**Class hierarchy:** *[Database](../Database.md)*


### Parameters ###

1. *array* `$arrTables`

	Associative array of tables to be locked

	```php
	<?php

	$arrTables = array('tl_news'=>'READ', 'tl_news_archive'=>'WRITE');
	$this->Database->lockTables($arrTables);