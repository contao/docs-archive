sysinit
-------

The `sysinit` hook is triggered right after the system initialization process is finished and before the request processing is started. It is available from version 3.1.0.


### Parameters ###

1. *Config* `$objConfig`

	The config object.


### Example ###

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['sysinit'][] = array('MyClass', 'mySysinit');

// MyClass.php
public function mySysinit(\Config $objConfig)
{
    $GLOBALS['TL_CONFIG']['customConfigKey'] = 'customConfigValue';
}
```


### References ###

- [system/initialize.php](https://github.com/contao/core/blob/3.1.0/system/initialize.php#L239)
