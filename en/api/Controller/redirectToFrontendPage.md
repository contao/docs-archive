
Controller :: redirectToFrontendPage
-------------------------------------------

Redirect to a front end page.


### Description ###

**Definition:** `protected function redirectToFrontendPage($intPage, $varArticle=null, $blnReturn=false)`

**Located in:** *system/libraries/Controller.php*

**Class hierarchy:** *[System](../System.php) > [Controller](../Controller.php)*


### Parameters ###

1. *integer* `$intPage`

	The numberic ID of the destination page.

2. *mixed* `$varArticle`

	Then numberic ID or alias of the article that should be appended to the URL.

3. *boolean* `$blnReturn`

	If set to true, the URL will be returned and redirect will be made.


### Return Values ###

If the ```$blnReturn``` is set to true, it will return an URL of the given page. Otherwise it will perform a redirect.


### Examples ###

1. Redirect to the page with ID of 123

	```php
	<?php

	$this->redirectToFrontendPage(123);
	```


### See Also ###

- [`Controller::generateFrontendUrl`](generateFrontendUrl.md) – Generate a front end URL
- [`Controller::convertRelativeUrls`](convertRelativeUrls.md) – Convert relative URLs to absolute
- [`Controller::addStaticUrlTo`](addStaticUrlTo.md) – Add a static URL to script
- [`Controller::setStaticUrl`](setStaticUrl.md) – Set a static URL
