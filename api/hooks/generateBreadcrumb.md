# generateBreadcrumb

The `generateBreadcrumb` hook is used to manipulate the breadcrumb navigation
(from breadcrumb front end module).


## Parameters

1. *array* `$arrItems`

    The breadcrumb navigation items.

2. *object* `$objModule`

    The front end module (ModuleBreadcrumb) instance.


## Return Values

Modify the list of breadcrumb items and return the items array.


## Example

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['generateBreadcrumb'][] = array('MyClass', 'myGenerateBreadcrumb');

// MyClass.php
public function myGenerateBreadcrumb($arrItems, $objModule)
{
    // Remove the first breadcrumb item, e.g. the "home" page.
    unset($arrItems[0]);

    return $arrItems;
}
```


## More information


### References

- [system/modules/frontend/ModuleBreadcrumb.php](https://github.com/contao/core/blob/2.11.7/system/modules/frontend/ModuleBreadcrumb.php#L222)


### See also

- [getUserNavigation](getUserNavigation.md) – modify the backend navigation

