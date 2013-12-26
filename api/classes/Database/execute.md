
Database :: execute
-------------------------------------------

Execute a query (return a Database_Result object).


### Description ###

**Definition:** `public function execute($strQuery)`

**Located in:** *system/libraries/Database.php*

**Class hierarchy:** *[Database](../Database.md)*


### Parameters ###

1. *string* `$strQuery`

	SQL query to be prepared and executed.


### Return Values ###

The Database_Result object.


### Examples ###

1. Prepare the statement and execute it

	```php
	<?php

	$objNews = $this->Database->prepare("SELECT * FROM tl_news WHERE pid=?")
	                          ->execute(4);