
Date :: getRegexp
-------------------------------------------

Return a regular expression to check a date.


### Description ###

**Definition:** `public function getRegexp($strFormat=false)`

**Located in:** *system/libraries/Date.php*

**Class hierarchy:** *[System](../System.md) > [Date](../Date.md)*


### Parameters ###

1. *string* `$strFormat`

	The optional date format. If none provided, the global format will be used - ```$GLOBALS['TL_CONFIG']['dateFormat']```.


### Return Values ###

A date converted to regular expression.

