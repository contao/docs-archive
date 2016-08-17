# sqlGetFromDB

The `sqlGetFromDB` hook is triggered when parsing the current database
definition. It passes the generated SQL definitions and expects the same
as return value.

> #### primary:: Available   
> from Contao 2.11.0-rc2.


## Parameters

1. *array* `$arrSql`

    The compiled SQL definitions.


## Return Values

Return `$arrSql` after adding your custom definitions.


## Example

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['sqlGetFromDB'][] = array('MyClass', 'mySqlGetFromDB');

// MyClass.php
public function mySqlGetFromDB($arrSql)
{
    // Modify the array of SQL statements

    return $arrSql;
}
```


## More information


### References

- [system/modules/core/library/Contao/Database/Installer.php](https://github.com/contao/core/blob/3.5.0/system/modules/core/library/Contao/Database/Installer.php#L535-L542)


### See also

- [sqlCompileCommands](sqlCompileCommands.md) – triggered when compiling the database update commands.
- [sqlGetFromFile](sqlGetFromFile.md) – triggered when parsing database.sql files.
- [sqlGetFromDca](sqlGetFromDca.md) – triggered when database definitions in DCA files are evaluated.
