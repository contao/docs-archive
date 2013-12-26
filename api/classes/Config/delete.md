
Config :: delete
-------------------------------------------

Delete a configuration variable from the local configuration file.


### Description ###

**Definition:** `public function delete($strKey)`

**Located in:** *system/libraries/Config.php*

**Class hierarchy:** *[Config](../Config.md)*


### Parameters ###

1. *string* `$strKey`

	Name of the variable.


### Examples ###

1. Delete the old variable

	```php
	<?php

	$this->Config->delete('oldVariable');