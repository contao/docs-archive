
Controller :: generateFrontendUrl
-------------------------------------------

Generate an URL from a tl_page record depending on the current rewriteURL setting and return it.


### Description ###

**Definition:** `protected function generateFrontendUrl($arrRow, $strParams=null, $strForceLanguage=null)`

**Located in:** *system/libraries/Controller.php*

**Class hierarchy:** *[System](../System.php) > [Controller](../Controller.php)*


### Parameters ###

1. *array* `$arrRow`

	Array with a record from tl_page. Most important fields are `id` and `alias`.

2. *string* `$strParams`

	Additional parameters to be added.

3. *string* `$strForceLanguage`

	Rewrite the URL to this language (if "add language to URL" is enabled in system config).


### Examples ###

1. Generate a regular frontend URL

	```php
	<?php

	$objPage = $this->Database->execute("SELECT * FROM tl_page WHERE id=1");
	$strUrl = $this->generateFrontendUrl($objPage->row());

	echo $strUrl;
	```
	> alias.html

2. Add additional parameters to the URL

	```php
	<?php

	$arrPage = array('id' => 7, 'alias' => 'news');
	$strUrl = $this->generateFrontendUrl($arrPage, '/items/example');

	echo $strUrl;
	```
	> news/items/example.html
