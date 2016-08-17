# replaceInsertTags

The `replaceInsertTags` hook is triggered when an unknown insert tag is found.
It passes the insert tag as argument and expects the replacement value or
false as return value.

> #### primary:: Available   
> from Contao 2.6.0.


## Parameters

1. *string* `$strTag`

  The unknown insert tag.


## Return Values

Return a string if your function is taking care of this insert tag. The hook loop
will be stopped and your output is used as a replacement value.

If your function is not responsible for this insert tag, you **must** return
`false` to continue to the next hook callback.


## Example

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['replaceInsertTags'][] = array('MyClass', 'myReplaceInsertTags');

// MyClass.php
public function myReplaceInsertTags($strTag)
{
    if ($strTag == 'mytag')
    {
        return 'mytag replacement';
    }

    return false;
}
```


## More information


### References

- [system/modules/core/library/Contao/InsertTags.php](https://github.com/contao/core/blob/3.5.0/system/modules/core/library/Contao/InsertTags.php#L1128-L1142)


### See also

- [addCustomRegexp](addCustomRegexp.md) - triggered when an unknown regular expression is found.
