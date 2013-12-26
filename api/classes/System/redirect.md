
System :: redirect
-------------------------------------------

Redirect to another page.


### Description ###

**Definition:** `protected function redirect($strLocation, $intStatus=303)`

**Located in:** *system/libraries/System*

**Class hierarchy:** *[System](../System.md)*


### Parameters ###

1. *string* `$strLocation`

	The destination URL.

2. *integer* `$intStatus`

	Header status.
	- **301** – 
		Moved Permanently.
	- **302** – 
		Found.
	- **303** *(default)* – 
		See Other.


### Examples ###

1. Redirect to the calendar page

	```php
	<?php

	$this->redirect('calendar.html');
	```

