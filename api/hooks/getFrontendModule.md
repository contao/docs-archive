# getFrontendModule

The `getFrontendModule` hook allows to manipulate the generation of the front end
modules.

> **Tag** Available from version 2.11.0-RC1.


## Parameters

1. *Database_Result* `$objRow`

    Database result of the frontend module.

2. *string* `$strBuffer`

    The generated frontend module buffer.



## Return Values

Return `$strBuffer` or your custom modification.


## Example

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['getFrontendModule'][] = array('MyClass', 'myGetFrontendModule');

// MyClass.php
public function myGetFrontendModule($objRow, $strBuffer)
{
    // Wrap all modules in an additional wrapper div
    return '<div class="module">' . $strBuffer . '</div>';
}
```


## More information


### References

- [system/libraries/Controller.php](https://github.com/contao/core/blob/2.11.7/system/libraries/Controller.php#L361)


### See also

- [getContentElement](getContentElement.md) – triggered when a content element is generated
- [getArticle](getArticle.md) – tiggered when an article is generated
- [getForm](getForm.md) – triggered when a form is generated

