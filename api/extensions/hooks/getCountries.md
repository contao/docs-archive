# getCountries

The `getCountries` hook allows to modify the system's list of countries.

> **Tag** Available from version 2.11.0-RC1.


## Parameters

1. *array* `$arrCountriesList`

    The array containing the countries as filled by `\System::getCountries()` according to the 
    system's configuration. This parameter has to be passed by reference.

2. *array* `$arrCountriesConfig`

    The list of countries from the system config file.


## Example

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['getCountries'][] = array('MyClass', 'myGetCountries');

// MyClass.php
public function myGetCountries(&$arrCountriesList, $arrCountriesConfig)
{
    // list of european countries
    $arrEurope = array('de', 'at', 'ch', ...);
   
    // remove all non-european countries
    $arrCountriesList = array_intersect_key($arrCountries, array_flip($arrEurope));
}
```


## More information


### References

- [system/modules/core/library/Contao/System.php](https://github.com/contao/core/blob/3.5.0/system/modules/core/library/Contao/System.php#L403-L409)


### See also

- [loadLanguageFile](loadLanguageFile.md) – triggered when a language file is loaded.
