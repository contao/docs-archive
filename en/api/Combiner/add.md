
Combiner :: add
-------------------------------------------

Add a file.


### Description ###

**Definition:** `public function add($strFile, $strVersion=null, $strMedia='screen')`

**Located in:** *system/libraries/Combiner.php*

**Class hierarchy:** *[System](System.md) > Combiner*


### Parameters ###

1. *string* `$strFile`

	A relative path of the file to be added. At the moment only .css and .js files are supported.

2. *string* `$strVersion`

	Default version of the file.

3. *string* `$strMedia`

	Media type of the file (defaults to *screen*).


### Examples ###

1. Add style files

	```php
	<?php

	$objCombiner = new Combiner();
	$objCombiner->add('tl_files/layout/reset.css');
	$objCombiner->add('tl_files/layout/styles.css');