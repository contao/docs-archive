# getFrontendModule

The `getFrontendModule` hook allows to manipulate the generation of the front end
modules.

> **Tag** Available from version 2.11.0-RC1.


## Parameters

1. *Database_Result* `$objRow`

    Database result of the front end module.

2. *string* `$strBuffer`

    The generated front end module buffer.



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

- [system/modules/core/library/Contao/Controller.php](https://github.com/contao/core/blob/3.5.0/system/modules/core/library/Contao/Controller.php#L316-L322)


### See also

- [getContentElement](getContentElement.md) – triggered when a content element is generated.
- [getArticle](getArticle.md) – tiggered when an article is generated.
- [getForm](getForm.md) – triggered when a form is generated.
- [isVisibleElement](isVisibleElement.md) – triggered when checking if an element should be visible in the front end or not.
