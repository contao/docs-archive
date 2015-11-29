# getLanguages

The `getLanguages` hook allows to modify the system's list of languages.

> **Tag** Available from version 3.3.RC1.


## Parameters

$languages, $langsNative, $blnInstalledOnly

1. *array* `$compiledLanguages`

    The array containing the languages as filled by `\System::getLanguages()` according 
    to the system's configuration. This parameter has to be passed by reference if you 
    want your changes to become effective.

2. *array* `$languages`

    The list of languages from the system config file `countries.php` with english
    language names.

3. *array* `$langsNative`
 
    The list of languages with native language names (also read from from the system 
    config file `countries.php`).
    
4. *boolean* `$blnInstalledOnly`
 
    Indicates whether only installed in the back end should be considered in the result. 


## Example

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['getCountries'][] = array('MyClass', 'myGetLanguages');

// MyClass.php
public function myGetLanguages(&$compiledLanguages, $languages, $langsNative, $blnInstalledOnly)
{
  // make your changes to $compiledLanguages
}
```


## More information


### References

- [system/modules/core/library/Contao/System.php](https://github.com/contao/core/blob/3.5.0/system/modules/core/library/Contao/System.php#L456-L462)
- [system/config/languages.php](https://github.com/contao/core/blob/3.5.0/system/config/languages.php)
