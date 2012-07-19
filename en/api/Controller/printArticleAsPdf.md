
Controller :: printArticleAsPdf
-------------------------------------------

Print an article as PDF and stream it to the browser.


### Description ###

**Definition:** `protected function printArticleAsPdf(Database_Result $objArticle)`

**Located in:** *system/libraries/Controller.php*

**Class hierarchy:** *[System](../System.php) > [Controller](../Controller.php)*


### Parameters ###

1. *Database_Result* `$objArticle`

	A database object that contains an article.


### Examples ###

1. Download the article with ID of 123 as PDF

	```php
	<?php

	$objArticle = $this->Database->prepare("SELECT * FROM tl_article WHERE id=?")->limit(1)->execute(123);
	$this->printArticleAsPdf($objArticle);
	```
	
