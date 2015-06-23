# replaceInsertTags


The `replaceInsertTags` hook is triggered when an unknown insert tag is found. It passes the insert tag as argument and expects the replacement value or false as return value. It is available from version 2.6.0.


## Parameters 

1. *string* `$strTag`

	the unknown inserttag


## Return Values 

Return a string if your function is taking care of this insert tag. The hook loop will be stopped and your output is used as a replacement value.

If your function is not responsible for this insert tag, you **must** return `false` to continue to the next hook callback.


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


## More Information


### References

- [system/libraries/Controller.php](https://github.com/contao/core/blob/2.11.7/system/libraries/Controller.php#L2432)


### See Also

- [addCustomRegexp](addCustomRegexp.md) - triggered when an unknown regular expression is found
