
Input :: setPost
-------------------------------------------

Set a $_POST parameter.


### Description ###

**Definition:** `public function setPost($strKey, $varValue)`

**Located in:** *system/libraries/Input.php*

**Class hierarchy:** *[Input](../Input.md)*


### Parameters ###

1. *string* `$strKey`

	Name of the $_GET property to be set.

2. *mixed* `$varValue`

	Value of the $_GET property to be set.


### Examples ###

1. Set a member parameter to 5

	```php
	<?php

	$this->Input->setPost('member', 5);
	```


### See Also ###

- [`Input::post`](post.md) – Return a $_POST parameter
- [`Input::postHtml`](postHtml.md) – Return a $_POST parameter preserving allowed HTML tags
- [`Input::postRaw`](postRaw.md) – Return a $_POST parameter unencoded without stripping tags
