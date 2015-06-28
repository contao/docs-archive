# getRootPageFromUrl

The `getRootPageFromUrl` hook is triggered when searching the current root page.
It does not pass any parameters, and expects a database result on success.


## Return Values

Return a database result from `tl_page` if you want to override the default method
for searching the root page.


## Example

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['getRootPageFromUrl'][] = array('MyClass', 'myGetRootPageFromUrl');

// MyClass.php
public function myGetRootPageFromUrl()
{
    // Do something
}
```


## More information


### References

- [system/modules/core/classes/Frontend.php](https://github.com/contao/core/blob/3.5.0/system/modules/core/classes/Frontend.php#L297-L307)


### See also

- [getPageIdFromUrl](getPageIdFromUrl.md) – triggered when the URL fragments are evaluated.
