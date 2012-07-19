
Controller :: getTemplate
-------------------------------------------

Find a particular template file and return its path.


### Description ###

**Definition:** `protected function getTemplate($strTemplate, $strFormat='html5')`

**Located in:** *system/libraries/Controller.php*

**Class hierarchy:** *[System](../System.php) > [Controller](../Controller.php)*

**Throws:** *Exception*


### Parameters ###

1. *string* `$strTemplate`

	A template name.

2. *string* `$strFormat`

	The template format.


### Return Values ###

A full template path.


### Examples ###

1. Get the template file path

	```php
	<?php

	$strTemplate = 'mod_newslist';
	echo $this->getTemplate('mod_newslist');
	```
	> /Applications/MAMP/htdocs/contao/system/modules/news/templates/mod_newslist.html5
	
2. Get the XHTML template file path

	```php
	<?php

	$strTemplate = 'mod_newslist';
	echo $this->getTemplate('mod_newslist', 'xhtml');
	```
	> /Applications/MAMP/htdocs/contao/system/modules/news/templates/mod_newslist.xhtml
