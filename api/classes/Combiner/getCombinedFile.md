
Combiner :: getCombinedFile
-------------------------------------------

Generate the combined file and return the path.


### Description ###

**Definition:** `public function getCombinedFile($strUrl=TL_SCRIPT_URL)`

**Located in:** *system/libraries/Combiner.php*

**Class hierarchy:** *[System](System.md) > Combiner*


### Parameters ###

1. *string* `$strUrl`

	Base path of the combined file.
	

### Return Values ###

A path to the combined file.


### Examples ###

1. Add combined style files to the page

	```php
	<?php

	$objCombiner = new Combiner();
	$objCombiner->add('tl_files/layout/reset.css');
	$objCombiner->add('tl_files/layout/styles.css');
	
	echo '<style type="text/css" src="' . $objCombiner->getCombinedFile() . '">';


