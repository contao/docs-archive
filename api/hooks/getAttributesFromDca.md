# getAttributesFromDca

The `getAttributesFromDca` hook is triggered when attributes of a Widget are
extracted from a Data Container Array. It passes the attributes and the DCA object
as arguments and expects the (modified) form attributes as return value.
It is available from version 3.2.0.


## Parameters

1. *array* `$arrAttributes`

	An array of Attributes ...

2. *object* `$objDca`

	The DataContainer object. It can be `null` if no object was passed 
	to the `Widget::getAttributesFromDca` method.


## Example

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['getAttributesFromDca'][] = array('MyClass', 'myGetAttributesFromDca');

// MyClass.php
public function myGetAttributesFromDca($arrAttributes, $objDca)
{
    // modify $arrAttributes as needed

    return $arrAttributes;
}
```


## More Information


### References

- [system/modules/core/library/Contao/Widget.php](https://github.com/contao/core/blob/support/3.2/system/modules/core/library/Contao/Widget.php#L1418)
