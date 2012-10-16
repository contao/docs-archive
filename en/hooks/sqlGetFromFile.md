sqlGetFromFile
--------------

The `sqlGetFromFile` hook is triggered when parsing database.sql files. It passes the generated SQL definition and expects the same as return value. Added in Contao 2.11.RC2.



### Parameters ###

1. *array* `$arrReturn`

	The parsed SQL definition.



### Return Values ###

Return `$arrReturn` after adding your custom definitions.


### Example ###

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['sqlGetFromFile'][] = array('MyClass', 'mySqlGetFromFile');

// MyClass.php
public function mySqlGetFromFile($arrReturn)
{
	// Modify the result
	
	return $arrReturn;
}
```


### See Also ###

- [sqlCompileCommands](sqlCompileCommands.md) – triggered when compiling the database update commands.
- [sqlGetFromDB](sqlGetFromDB.md) … triggered when parsing the current database definition
