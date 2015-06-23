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

- [system/modules/backend/DbInstaller.php](https://github.com/contao/core/blob/2.11.7/system/modules/backend/DbInstaller.php#L418)


### See also

- [sqlCompileCommands](sqlCompileCommands.md) – triggered when compiling the database update commands.
- [sqlGetFromFile](sqlGetFromFile.md) – triggered when parsing database.sql files
