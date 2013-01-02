
Input :: postHtml
-------------------------------------------

Return a $_POST parameter preserving allowed HTML tags.


### Description ###

**Definition:** `public function postHtml($strKey, $blnDecodeEntities=false)`

**Located in:** *system/libraries/Input.php*

**Class hierarchy:** *[Input](../Input.md)*


### Parameters ###

1. *string* `$strKey`

	Name of the $_POST parameter to be returned.

2. *boolean* `$blnDecodeEntities`

	If true, the entities will be decoded. Defaults to false.


### Return Values ###

Mixed values.


### See Also ###

- [`Input::post`](post.md) – Return a $_POST parameter
- [`Input::postRaw`](postRaw.md) – Return a $_POST parameter unencoded without stripping tags
- [`Input::setPost`](setPost.md) – Set a $_POST parameter




