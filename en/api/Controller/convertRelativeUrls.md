
Controller :: convertRelativeUrls
-------------------------------------------

Convert relative URLs to absolute URLs in the provided string.


### Description ###

**Definition:** `protected function convertRelativeUrls($strContent, $strBase='', $blnHrefOnly=false)`

**Located in:** *system/libraries/Controller.php*

**Class hierarchy:** *[System](../System.php) > [Controller](../Controller.php)*


### Parameters ###

1. *string* `$strContent`

	A string to be parsed.

2. *string* `$strBase`

	The base of newly created URLs.

3. *boolean* `$blnHrefOnly`

	If set to true, it will parse *href* attributes and omit the *src* attributes.


### Return Values ###

A string with converted relative to absolute URLs.


### Examples ###

1. Convert relative URLs to absolute

	```php
	<?php

	$strLink = '<a href="news.html">News</a>';
	echo $this->convertRelativeUrls($strLink);
	```
	> ```<a href="http://www.example.com/news.html">News</a>```

