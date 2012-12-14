
Database :: getInstance
-------------------------------------------

Instantiate a database driver object and return it (Factory).


### Description ###

**Definition:** `public static function getInstance()`

**Located in:** *system/libraries/Database.php*

**Class hierarchy:** *[Database](../Database.md)*

**Throws:** *Exception*


### Return Values ###

The database instance.


### Examples ###

1. Get all news items

	```php
	<?php

	$objNews = Database::getInstance()->query("SELECT * FROM tl_news");
	```

