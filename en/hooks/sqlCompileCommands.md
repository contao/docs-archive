sqlCompileCommands
------------------

The `sqlCompileCommands` hook is triggered when compiling the database update commands. It passes the array of changes and expects the same as return value. Added in Contao 2.11.RC2.


### Parameters ###

1. *array* `$arrReturn`

	Array of changes that should be applied to the database.


### Return Values ###

Return the array of changes that should be applied to the database.


### Example ###

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['sqlCompileCommands'][] = array('MyClass', 'mySqlCompileCommands');

// MyClass.php
public function mySqlCompileCommands($arrReturn)
{
	// Modify the result
	
	return $arrReturn;
}
```


### See Also ###

- [sqlGetFromDB](sqlGetFromDB.md) … triggered when parsing the current database definition
- [sqlGetFromFile](sqlGetFromFile.md) – triggered when parsing database.sql files
