# createDefinition

The `createDefinition` hook is triggered when a format definition of a style
sheet is imported. It passes the key and value, the original format definition
and the data array as arguments and expects an array or `false` as return value.

> #### tag:: Version Information 
> Available from Contao version 2.9.4.


## Example

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


## More information


### References

- [system/modules/core/classes/StyleSheets.php](https://github.com/contao/core/blob/3.5.0/system/modules/core/classes/StyleSheets.php#L2230-L2243)


### See also

- [compileDefinition](compileDefinition.md) - triggered when a format definition of a style sheet is written.
