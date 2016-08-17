# reviseTable

The `reviseTable` hook is triggered when Contao removes orphan records from a
table. It passes the name of the current table, the IDs of all new records, the
name of the parent table and the names of all child tables as arguments and
does expect a boolean as return value (returning `true` will cause the current
page to be reloaded).

> #### primary:: Available   
> from Contao 2.6.4.


## Example

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['reviseTable'][] = array('MyClass', 'myReviseTable');

// MyClass.php
public function myReviseTable($table, $new_records, $parent_table, $child_tables)
{
    // Do something
}
```


## More information


### References

- [system/modules/core/drivers/DC_Table.php](https://github.com/contao/core/blob/3.5.0/system/modules/core/drivers/DC_Table.php#L3138-L3159)


### See also

- [removeOldFeeds](removeOldFeeds.md) – triggered when old XML files are being removed from the Contao root directory.
