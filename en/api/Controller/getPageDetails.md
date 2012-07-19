
Controller :: getPageDetails
-------------------------------------------

Get the details of a page including inherited parameters and return it as object or null, if not found.


### Description ###

**Definition:** `protected function getPageDetails($intId)`

**Located in:** *system/libraries/Controller.php*

**Class hierarchy:** *[System](../System.php) > [Controller](../Controller.php)*


### Parameters ###

1. *integer* `$intId`

	The numberic ID of the page.


### Return Values ###

A Database_Result object containing the page, or null if the page is not found.


### Examples ###

1. Display the name of the page with ID of 123.

	```php
	<?php

	$objPage = $this->getPageDetails(123);
	echo $objPage->title;
	```
	> Academy News

