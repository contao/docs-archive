# getFrontendModule

The `getFrontendModule` hook allows to manipulate the generation of the front end
modules.

> #### primary:: Available   
> from Contao 2.11.0-RC1.


## Parameters

1. *ModuleModel* `$objRow`

    Database result of the front end module

2. *string* `$strBuffer`

    The generated front end module buffer.
    
3. *Module* `$objModule`

    The class of the front end module. (Inherit from `Module`)


## Return Values

Return `$strBuffer` or your custom modification.


## Changelog

Version | Description
--------|------------
3.0     | Changed `$objRow` type from *Database_Result* to *ModuleModel*. Added `$objModule` parameter.


## Example

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['getFrontendModule'][] = array('MyClass', 'myGetFrontendModule');

// MyClass.php
public function myGetFrontendModule($objRow, $strBuffer, $objModule)
{
    // Wrap all modules in an additional wrapper div
    return '<div class="module">' . $strBuffer . '</div>';
}
```


## More information


### References

- Contao 3.5: [system/modules/core/library/Contao/Controller.php](https://github.com/contao/core/blob/3.5.0/system/modules/core/library/Contao/Controller.php#L316-L322)

- Contao 4.4: [src/Resources/contao/library/Contao/Controller.php](https://github.com/contao/core-bundle/blob/b79c03bcd9a1d9eea1150ff88a55e67e7f1e52c1/src/Resources/contao/library/Contao/Controller.php#L329)

### See also

- [getContentElement](getContentElement.md) – triggered when a content element is generated.
- [getArticle](getArticle.md) – tiggered when an article is generated.
- [getForm](getForm.md) – triggered when a form is generated.
- [isVisibleElement](isVisibleElement.md) – triggered when checking if an element should be visible in the front end or not.
