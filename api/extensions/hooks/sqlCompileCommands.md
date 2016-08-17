# sqlCompileCommands

The `sqlCompileCommands` hook is triggered when compiling the database update
commands. It passes the array of changes and expects the same as return value.

> #### primary:: Available   
> from Contao 2.11.0-rc2.


## Parameters

1. *array* `$arrSql`

    Array of changes that should be applied to the database.


## Return Values

Return the array of changes that should be applied to the database.


## Example

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['sqlCompileCommands'][] = array('MyClass', 'mySqlCompileCommands');

// MyClass.php
public function mySqlCompileCommands($arrSql)
{
    // Modify the array of SQL statements

    return $arrSql;
}
```


## More information


### References

- [system/modules/core/library/Contao/Database/Installer.php](https://github.com/contao/core/blob/3.5.0/system/modules/core/library/Contao/Database/Installer.php#L242-L249)


### See also

- [sqlGetFromDB](sqlGetFromDB.md) – triggered when parsing the current database definition.
- [sqlGetFromDca](sqlGetFromDca.md) – triggered when database definitions in DCA files are evaluated.
- [sqlGetFromFile](sqlGetFromFile.md) – triggered when parsing database.sql files.
