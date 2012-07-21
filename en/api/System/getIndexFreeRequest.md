
System :: getIndexFreeRequest
-------------------------------------------

Return the request string or an empty string if the request string is "index.php" and optionally encode ampersands.


### Description ###

**Definition:** `protected function getIndexFreeRequest($blnAmpersand=true)`

**Located in:** *system/libraries/System*

**Class hierarchy:** *[System](../System.md)*


### Parameters ###

1. *boolean* `$blnAmpersand`

	If set to true, the returned URL will be ampersanded.


### Return Values ###

The current request string or an empty string if the request string is "index.php".


### Examples ###

1. Set the form action parameter

	```php
	<?php

	// ModuleCustom.php
	$this->Template->action = $this->getIndexFreeRequest();

	// mod_custom.html5
	<form action="<?php echo $this->action; ?>" method="post">
	```

