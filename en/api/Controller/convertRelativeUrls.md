
Controller :: convertRelativeUrls
-------------------------------------------

Convert relative URLs to absolute URLs in the provided string.


### Description ###

**Definition:** `protected function convertRelativeUrls($strContent, $strBase='', $blnHrefOnly=false)`

**Located in:** *system/libraries/Controller.php*

**Class hierarchy:** *[System](../System.md) > [Controller](../Controller.md)*


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


### See Also ###

- [`Controller::generateFrontendUrl`](generateFrontendUrl.md) – Generate a front end URL
- [`Controller::redirectToFrontendPage`](redirectToFrontendPage.md) – Redirect to a front end page
- [`Controller::addStaticUrlTo`](addStaticUrlTo.md) – Add a static URL to script
- [`Controller::setStaticUrl`](setStaticUrl.md) – Set a static URL
