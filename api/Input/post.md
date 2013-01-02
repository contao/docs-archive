
Input :: post
-------------------------------------------

Return a $_POST parameter.


### Description ###

**Definition:** `public function post($strKey, $blnDecodeEntities=false)`

**Located in:** *system/libraries/Input.php*

**Class hierarchy:** *[Input](../Input.md)*


### Parameters ###

1. *string* `$strKey`

	Name of the $_POST parameter to be returned.

2. *boolean* `$blnDecodeEntities`

	If true, the entities will be decoded. Defaults to false.


### Return Values ###

Mixed values.


### Examples ###

1. Check if the form was submitted

	```php
	<?php

	if ($this->Input->post('FORM_SUBMIT') == 'my_form')
	{
		// Process the form
	}
	```


### See Also ###

- [`Input::postHtml`](postHtml.md) – Return a $_POST parameter preserving allowed HTML tags
- [`Input::postRaw`](postRaw.md) – Return a $_POST parameter unencoded without stripping tags
- [`Input::setPost`](setPost.md) – Set a $_POST parameter
