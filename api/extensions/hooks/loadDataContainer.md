# loadDataContainer

The `loadDataContainer` hook is triggered when a DCA file is loaded. It passes
the file name as argument and does not expect a return value.

> #### primary:: Available   
> from Contao 2.8.2.


## Parameters

1. *string* `$strName`

    Name of the data container to be loaded (e.g. `tl_content`).


## Example

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['loadDataContainer'][] = array('MyClass', 'myLoadDataContainer');

// MyClass.php
public function myLoadDataContainer($strName)
{
    // Do something
}
```


## More information


### References

- [system/modules/core/library/Contao/DcaLoader.php](https://github.com/contao/core/blob/3.5.0/system/modules/core/library/Contao/DcaLoader.php#L92-L99)


### See also

- [loadLanguageFile](loadLanguageFile.md) - triggered when a language file is loaded.
