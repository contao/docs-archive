# sqlGetFromDB

The `sqlGetFromDB` hook is triggered when parsing the current database
definition. It passes the generated SQL definitions and expects the same
as return value.

> **Tag** Available from version 2.11.0-RC2.


## Parameters

1. *array* `$arrReturn`

    The compiled SQL definitions.


## Return Values

Return `$arrReturn` after adding your custom definitions.


## Example

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


## More information


### References

- [system/modules/core/library/Contao/Database/Installer.php](https://github.com/contao/core/blob/3.5.0/system/modules/core/library/Contao/Database/Installer.php#L535-L542)


### See also

- [sqlCompileCommands](sqlCompileCommands.md) – triggered when compiling the database update commands.
- [sqlGetFromFile](sqlGetFromFile.md) – triggered when parsing database.sql files.
