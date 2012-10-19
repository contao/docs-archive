
Database :: query
-------------------------------------------

Execute a raw query (return a Database_Result object).


### Description ###

**Definition:** `public function query($strQuery)`

**Located in:** *system/libraries/Database.php*

**Class hierarchy:** *[Database](../Database.md)*


### Parameters ###

1. *string* `$strQuery`

	SQL query to be prepared and executed.


### Return Values ###

The Database_Result object.


### Examples ###

1. Get all news

	```php
	<?php

	$objNews = $this->Database->query("SELECT * FROM tl_news");