# getCountries

The `getCountries` hook allows to modify the system's list of countries.

> **Tag** Available from version 2.11.0-RC1.


## Parameters

1. *array* `$arrReturn`

    Empty array that should be used to add custom entries.

2. *array* `$arrCountries`

    The list of countries from the system config file.


## Return Values

Return an array with additional countries you want to add.


## Examples

1. Add custom countries to the options. They are added **before** the system countries.

    ```php
    <?php

    // config.php
    $GLOBALS['TL_HOOKS']['getCountries'][] = array('MyClass', 'myGetCountries');

    // MyClass.php
    public function myGetCountries(&$arrReturn, $arrCountries)
    {
        $arrReturn['oo'] = 'Moon';

    }
    ```

2. Modify the list of countries. This is not really intended by the hook, but it
can still be done by using a reference on the countries array.

    ```php
    <?php

    // config.php
    $GLOBALS['TL_HOOKS']['getCountries'][] = array('MyClass', 'myGetCountries');

    // MyClass.php
    public function myGetCountries($arrReturn, &$arrCountries)
    {
        // European Countries
        $arrEU = array('de', 'at', 'nl', ...);

        // Remove all non-EU countries
        $arrCountries = array_intersect_key($arrCountries, array_flip($arrEU));

    }
    ```


## More information


### References

- [system/modules/core/library/Contao/System.php](https://github.com/contao/core/blob/3.5.0/system/modules/core/library/Contao/System.php#L403-L409)


### See also

- [loadLanguageFile](loadLanguageFile.md) – triggered when a language file is loaded.
