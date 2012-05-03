createDefinition
----------------

The `createDefinition` hook is triggered when a format definition of a style sheet is imported. It passes the key and value, the original format definition and the data array as arguments and expects an array or false as return value. It is available from version 2.9.4.


### Example ###

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['createDefinition'][] = array('MyClass', 'myCreateDefinition');

// MyClass.php
public function myCreateDefinition($strKey, $strValue, $strDefinition, $arrSet)
{
    if ($strKey == 'border-radius')
    {
        return array('border-radius'=>$strValue);
    }

    return false;
}
```


### See Also ###

- [compileDefinition](compileDefinition.md) - triggered when a format definition of a style sheet is written