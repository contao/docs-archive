# getPageIdFromUrl

The `getPageIdFromUrl` hook is triggered when the URL fragments are evaluated.
It passes the array of URL fragments as argument and expects an array of URL
fragments as return value.

> #### primary:: Available   
> from Contao 2.5.4.


## Parameters

1. *array* `$arrFragments`

    The URL fragments (current url exploded by slash). Be aware that previous hook
    callbacks could have modified this data.


## Return Values

Return the (modified) array of URL fragments.


## Example

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['getPageIdFromUrl'][] = array('MyClass', 'myGetPageIdFromUrl');

// MyClass.php
public function myGetPageIdFromUrl($arrFragments)
{
    return array_unique($arrFragments);
}
```


## More information


### References

- [system/modules/core/classes/Frontend.php](https://github.com/contao/core/blob/3.5.0/system/modules/core/classes/Frontend.php#L236-L242)


### See also

- [getRootPageFromUrl](getRootPageFromUrl.md) – triggered when searching for the current root page.
- [getCacheKey](getCacheKey.md) – triggered when creating a page cache.
