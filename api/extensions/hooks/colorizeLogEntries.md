# colorizeLogEntries

The `colorizeLogEntries` hook is triggered when log entries are being
colorized depending on their category.

> #### warning:: Warning 
> You can not colorize log entries of the categories `CONFIGURATION`, 
> `REPOSITORY`, `CRON` and `ERROR` as the hook will not be called for these types.  

<!-- blockquote break -->

> #### tag:: Version Information 
> Available from Contao version 3.3.RC1.


## Parameters

1. *string* `$row`

    The data of the log entry record.

2. *string* `$label`

    The label as created by Contao. If not modified by this hook, this
    is what will be displayed.


## Return Values

Return the modified `$label`.


## Example

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['colorizeLogEntries'][] = array('MyClass', 'myColorizeLogEntries');

// MyClass.php
public function myColorizeLogEntries($row, $label)
{
    // highlight logins ...
    
    if ($row['func'] == 'Contao\User::login') {
        $label = "<span class='tl_orange'>$label</span>";
    }

    // ... and visualize the source next to the date of the log entry
    
    return preg_replace('/(.+?)\]/', "$1 " . $row['source'] . ']', $label);
}
```


## More information


### References

- [system/modules/core/dca/tl_log.php](https://github.com/contao/core/blob/3.5.0/system/modules/core/dca/tl_log.php#L181-L188)
