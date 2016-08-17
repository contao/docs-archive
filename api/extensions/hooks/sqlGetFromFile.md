# sqlGetFromFile

The `sqlGetFromFile` hook is triggered when parsing database.sql files. It passes
the generated SQL definition and expects the same as return value.

> #### primary:: Available   
> from Contao 2.11.0-rc2.



## Parameters

1. *array* `$arrSql`

    The parsed SQL definition.



## Return Values

Return `$arrSql` after adding your custom definitions.


## Example

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['sqlGetFromFile'][] = array('MyClass', 'mySqlGetFromFile');

// MyClass.php
public function mySqlGetFromFile($arrSql)
{
    // Modify the array of SQL statements

    return $arrSql;
}
```


## More information


### References

- [system/modules/core/library/Contao/Database/Installer.php](https://github.com/contao/core/blob/3.5.0/system/modules/core/library/Contao/Database/Installer.php#L405-L412)


### See also

- [sqlCompileCommands](sqlCompileCommands.md) – triggered when compiling the database update commands.
- [sqlGetFromDB](sqlGetFromDB.md) – triggered when parsing the current database definition.
- [sqlGetFromDca](sqlGetFromDca.md) – triggered when database definitions in DCA files are evaluated.
