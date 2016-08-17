# initializeSystem

The `initializeSystem` hook is triggered right after the system initialization
process is finished and before the request processing is started.

> #### primary:: Available   
> from Contao 3.1.0.


## Example

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['initializeSystem'][] = array('MyClass', 'myInitializeSystem');

// MyClass.php
public function myInitializeSystem()
{
    $GLOBALS['TL_CONFIG']['customConfigKey'] = 'customConfigValue';
}
```


## More information


### References

- [system/initialize.php](https://github.com/contao/core/blob/3.5.0/system/initialize.php#L239-L245)
