loadDataContainer
-----------------

The `loadDataContainer` hook is triggered when a DCA file is loaded. It passes the file name as argument and does not expect a return value. It is available from version 2.8.2.


### Parameters ###

1. *string* `$strName`

	Name of the data container to be loaded (e.g. `tl_content`).


### Example ###

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


### See Also ###

- [loadLanguageFile](loadLanguageFile.md) - triggered when a language file is loaded
