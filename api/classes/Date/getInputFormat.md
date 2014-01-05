
Date :: getInputFormat
-------------------------------------------

Return an input format string for a particular date (e.g. YYYY-MM-DD).


### Description ###

**Definition:** `public function getInputFormat($strFormat=false)`

**Located in:** *system/libraries/Date.php*

**Class hierarchy:** *[System](../System.md) > [Date](../Date.md)*


### Parameters ###

1. *string* `$strFormat`

	The optional date format. If none provided, the global format will be used - ```$GLOBALS['TL_CONFIG']['dateFormat']```;


### Return Values ###

An input format for a particular date.


### See Also ###

- [`Date::formatToJs`](formatToJs.md) – Convert a PHP format string into a JavaScript format string