# sqlGetFromFile

The `sqlGetFromFile` hook is triggered when parsing database.sql files. It passes
the generated SQL definition and expects the same as return value.

> **Tag** Available from version 2.11.0-RC2.



## Parameters

1. *array* `$arrReturn`

    The parsed SQL definition.



## Return Values

Return `$arrReturn` after adding your custom definitions.


## Example

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


## More information


### References

- [system/modules/core/library/Contao/Database/Installer.php](https://github.com/contao/core/blob/3.5.0/system/modules/core/library/Contao/Database/Installer.php#L405-L412)


### See also

- [sqlCompileCommands](sqlCompileCommands.md) – triggered when compiling the database update commands.
- [sqlGetFromDB](sqlGetFromDB.md) – triggered when parsing the current database definition.
