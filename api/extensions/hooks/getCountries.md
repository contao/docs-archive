# getCountries

The `getCountries` hook allows to modify the system's list of countries.

> #### primary:: Available   
> from Contao 2.11.0-RC1.


## Parameters

1. *array* `$translatedCountries`

    The array containing the countries as filled by `\System::getCountries()` according to the 
    system's configuration. This parameter has to be passed by reference if you want your changes
     to become effective.

2. *array* `$allCountries`

    The list of countries from the system config file `countries.php`.


## Example

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['getCountries'][] = array('MyClass', 'myGetCountries');

// MyClass.php
public function myGetCountries(&$translatedCountries, $allCountries)
{
    // codes for the european countries
    $europeanCountryCodes = array('de', 'at', 'ch' /*, ... */);
   
    // remove all non-european countries
    $translatedCountries = array_intersect_key($translatedCountries, array_flip($europeanCountryCodes));
}
```


## More information


### References

- [system/modules/core/library/Contao/System.php](https://github.com/contao/core/blob/3.5.0/system/modules/core/library/Contao/System.php#L403-L409)
- [system/config/countries.php](https://github.com/contao/core/blob/3.5.0/system/config/countries.php)


### See also

- [loadLanguageFile](loadLanguageFile.md) – triggered when a language file is loaded.
