
Database :: prepare
-------------------------------------------

Prepare a statement (return a Database_Statement object).


### Description ###

**Definition:** `public function prepare($strQuery)`

**Located in:** *system/libraries/Database.php*

**Class hierarchy:** *[Database](../Database.md)*


### Parameters ###

1. *string* `$strQuery`

	SQL query to be prepared.


### Return Values ###

The Database_Statement object.


### Examples ###

1. Prepare the statement and execute it

	```php
	<?php

	$objNews = $this->Database->prepare("SELECT * FROM tl_news WHERE pid=?")
	                          ->execute(4);