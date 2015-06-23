# getUserNavigation

The `getUserNavigation` hook allows to manipulate the back end user navigation.
It passes the back end modules and a flag wether to show collapsed navigation
items. Expects the array of modules as return value.


## Parameters

1. *array* `$arrModules`

    The compiled list of back end modules.

2. *boolean* `$blnShowAll`

    Wether to show all modules even if the group is collapsed.


## Return Values

Add your custom modules to the list and return the array of back end modules.


## Example

```php
<?php
// config.php
$GLOBALS['TL_HOOKS']['getUserNavigation'][] = array('MyClass', 'myGetUserNavigation');

// MyClass.php
public function myGetUserNavigation($arrModules, $blnShowAll)
{
    // Add custom navigation item to the Contao website
    $arrModules['system']['modules']['contao'] = array
    (
        'label'		=> 'Contao Homepage',
        'title'		=> 'Visit the Contao CMS website',
        'class'		=> 'navigation contao',
        'href'		=> 'http://www.contao.org/',
    );

    return $arrModules;
}
```


## More information


### References

- [system/modules/backend/BackendUser.php](https://github.com/contao/core/blob/2.11.7/system/modules/backend/BackendUser.php#L468)


### See also

- [getSystemMessages](getSystemMessages.md) – allows to add additional messages to the back end home screen
