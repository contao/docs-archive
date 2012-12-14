
Combiner :: hasEntries
-------------------------------------------

Return true if there are files.


### Description ###

**Definition:** `public function hasEntries()`

**Located in:** *system/libraries/Combiner.php*

**Class hierarchy:** *[System](System.md) > Combiner*


### Return Values ###

Returns true if there are already files added, false otherwise.


### Examples ###

1. Add entries if there are none

	```php
	<?php

	if (!$objCombiner->hasEntries())
	{
		$objCombiner->add('tl_files/layout/reset.css');
		$objCombiner->add('tl_files/layout/styles.css');
	};