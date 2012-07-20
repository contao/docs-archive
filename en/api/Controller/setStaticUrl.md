
Controller :: setStaticUrl
-------------------------------------------

Set a static URL constant and replace the protocol when requested via SSL.


### Description ###

**Definition:** `protected function setStaticUrl($name, $url)`

**Located in:** *system/libraries/Controller.php*

**Class hierarchy:** *[System](../System.php) > [Controller](../Controller.php)*


### Parameters ###

1. *string* `$name`

	The constant name.

2. *string* `$url`

	The URL to be set as constant.


### See Also ###

- [`Controller::addStaticUrlTo`](addStaticUrlTo.md) – Add a static URL to script
- [`Controller::generateFrontendUrl`](generateFrontendUrl.md) – Generate a front end URL
- [`Controller::convertRelativeUrls`](convertRelativeUrls.md) – Convert relative URLs to absolute
- [`Controller::redirectToFrontendPage`](redirectToFrontendPage.md) – Redirect to a front end page
