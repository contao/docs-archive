sqlGetFromDB
------------

The `sqlGetFromDB` hook is triggered when parsing the current database definition. It passes the generated SQL definitions and expects the same as return value. Added in Contao 2.11.RC2.


### Parameters ###

1. *array* `$arrReturn`

	The compiled SQL definitions.


### Return Values ###

Return `$arrReturn` after adding your custom definitions.


### Example ###

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['sqlGetFromDB'][] = array('MyClass', 'mySqlGetFromDB');

// MyClass.php
public function mySqlGetFromDB($arrReturn)
{
	// Modify the result
	
	return $arrReturn;
}
```


### See Also ###

- [sqlCompileCommands](sqlCompileCommands.md) – triggered when compiling the database update commands.
- [sqlGetFromFile](sqlGetFromFile.md) – triggered when parsing database.sql files
