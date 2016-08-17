# loadLanguageFile

The `loadLanguageFile` hook is triggered when a language file is loaded. It
passes the file name and the language as arguments and does not expect a
return value.

> #### primary:: Available   
> from Contao 2.8.0-RC1.


## Parameters

1. *string* `$strName`

    The language file to be loaded (e.g. `tl_content`), without file extension.

2. *string* `$strLanguage`

    The language, usually the same as `$GLOBALS['TL_LANGUAGE']` but the call to
    `Controller::loadLanguageFile` accepts a language parameter.


## Example

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['loadLanguageFile'][] = array('MyClass', 'myLoadLanguageFile');

// MyClass.php
public function myLoadLanguageFile($strName, $strLanguage)
{
    // Do something
}
```


## More information


### References

- [system/modules/core/library/Contao/System.php](https://github.com/contao/core/blob/3.5.0/system/modules/core/library/Contao/System.php#L336-L342)


### See also

- [loadDataContainer](loadDataContainer.md) - triggered when a DCA file is loaded.
