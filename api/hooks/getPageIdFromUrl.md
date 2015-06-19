# getPageIdFromUrl


The `getPageIdFromUrl` hook is triggered when the URL fragments are evaluated. It passes the array of URL fragments as argument and expects an array of URL fragments as return value. It is available from version 2.5.4.


## Parameters 

1. *array* `$arrFragments`

	The URL fragments (current url exploded by slash). Be aware that previous hook callbacks could have modified this data.


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


## More Information


### References

- [system/modules/frontend/Frontend.php](https://github.com/contao/core/blob/2.11.7/system/modules/frontend/Frontend.php#L130)


### See Also

- [getRootPageFromUrl](getRootPageFromUrl.md) – triggered when searching for the current root page
- [getCacheKey](getCacheKey.md) – triggered when creating a page cache

