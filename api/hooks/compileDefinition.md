# compileDefinition


The `compileDefinition` hook is triggered when a format definition of a style sheet is written. It passes the configuration array as argument and expects a string as return value. It is available from version 2.9.4.


## Parameters 

1. *array* `$arrRow`

	The style definition database record


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


## More Information


### References

- [system/modules/backend/StyleSheets.php](https://github.com/contao/core/blob/2.11.7/system/modules/backend/StyleSheets.php#L1014)


### See Also

