
System :: addToUrl
-------------------------------------------

Add a request string to the current URI string.


### Description ###

**Definition:** `protected function addToUrl($strRequest)`

**Located in:** *system/libraries/System*

**Class hierarchy:** *[System](../System.md)*


### Parameters ###

1. *string* `$strClass`

	Additional parameters that should be added to the URL.


### Return Values ###

The current URL with appended parameters.


### Examples ###

1. Add *item/123* to the current URL

	```php
	<?php

	echo $this->addToUrl('item=123');
	```
	> index.php/index/item/123.html

