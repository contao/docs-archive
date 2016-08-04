# compileDefinition

The `compileDefinition` hook is triggered when a format definition of a style
sheet is written. It passes the configuration array as argument and expects a
string as return value.

> #### tag:: Version Information 
> Available from Contao version 2.9.4.


## Parameters

1. *array* `$arrRow`

    The style definition database record.


## Example

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['compileDefinition'][] = array('MyClass', 'myCompileDefinition');

// MyClass.php
public function myCompileDefinition($arrRow)
{
    if (isset($arrRow['border-radius']))
    {
        return "\nborder-radius:" . $arrRow['border-radius'] . ";";
    }

    return '';
}
```


## More information


### References

- [system/modules/core/classes/StyleSheets.php](https://github.com/contao/core/blob/3.5.0/system/modules/core/classes/StyleSheets.php#L939-L951)


### See also

- [createDefinition](createDefinition.md) - triggered when a format definition of a style sheet is imported.
