
Controller :: loadDataContainer
-------------------------------------------

Load a set of DCA files.


### Description ###

**Definition:** `protected function loadDataContainer($strName, $blnNoCache=false)`

**Located in:** *system/libraries/Controller.php*

**Class hierarchy:** *[System](../System.md) > [Controller](../Controller.md)*


### Parameters ###

1. *string* `$strName`

	Name of the data container to be loaded.

1. *boolean* `$blnNoCache`

	If set to true, the cache will not be used.


### Examples ###

1. Display the tl_news parent table

	```php
	<?php

	$this->loadDataContainer('tl_news');
	echo $GLOBALS['TL_DCA']['tl_news']['config']['ptable'];
	```
	> tl_news_archive
