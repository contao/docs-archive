# insertTagFlags

The `insertTagFlags` hook is triggered when unknown flags (filters) are passed
to an insert tag. It passes the arguments listed belows and expects the replacement
text as return value or `false` if the flag was not handled.

> #### primary:: Available   
> from Contao 3.1.0.


## Parameters

1. *boolean* `$flag`

    The name of the insert tag flag.

2. *string* `$cachedValue`

    The cached replacement for this insert tag (if there is any).

3. *array* `$flags`

    An array of flags used with this insert tag.

4. *boolean* `$blnCache`

   Indicates if we are supposed to cache.

5. *array* `$tags`

    Contains the result of spliting the page's content in order to replace the insert tags.

6. *array* `$arrCache`

   The cached replacements of insert tags found on the page so far.

7. *int* `$_rit`

    Counter used while iterating over the parts in `$tags`.

8. *int* `$_cnt`

    Number of elements in `$tags`.


## Return Values

The return value should be the replacement text or `false` if the flag was not handled.


## Example

If you use `{{date::D d. F Y|monthnamesAT|utf8_strtoupper}}` Contao knows how to handle
the `date` insert tag and the `utf8_strtoupper` flag. The unknown `monthnamesAT` triggers the hook:

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['insertTagFlags'][] = array('MyClass', 'myInsertTagFlags');

// MyClass.php
public function myInsertTagFlags($flag, $tag, $cachedValue, $flags, $blnCache, $tags, $arrCache, $_rit, $_cnt)
{
    if ($flag === 'monthnamesAT') {

        return str_replace(array("Januar","Februar"), array("Jänner", "Feber"), $cachedValue);

    }

    return false; // indicate that we did not handle that flag
}
```


## More Information


### References

- [system/modules/core/library/Contao/Controller.php](https://github.com/contao/core/blob/support/3.2/system/modules/core/library/Contao/Controller.php#L1779)
- [system/modules/core/library/Contao/InsertTags.php](https://github.com/contao/core/blob/3.5.0/system/modules/core/library/Contao/InsertTags.php#L1205)


### See Also

- [replaceInsertTags](replaceInsertTags.md) - triggered when an unknown insert tag is found.
