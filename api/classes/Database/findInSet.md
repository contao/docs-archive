
Database :: findInSet
-------------------------------------------

Auto-generate a FIND_IN_SET() statement.


### Description ###

**Definition:** `public function findInSet($strKey, $varSet, $blnIsField=false)`

**Located in:** *system/libraries/Database.php*

**Class hierarchy:** *[Database](../Database.md)*


### Parameters ###

1. *string* `$strKey`

	Key to be used as first parameter.

2. *mixed* `$varSet`

	Set to be searched in.

3. *boolean* `$blnIsField`

	Mark the set as field. False by default.


### Return Values ###

Ready to use FIND_IN_SET() query statement.


### Examples ###

1. Get the news sorted by parent IDs

	```php
	<?php

	$arrParentIds = array(1, 2, 3);
	$objNews = $this->Database->execute("SELECT * FROM tl_news ORDER BY " . $this->Database->findInSet('pid', $arrParentIds));