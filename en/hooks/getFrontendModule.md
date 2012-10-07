getFrontendModule
-----------------

The `getFrontendModule` hook allows to manipulate the generation of the frontend modules. Added in Contao 2.11.RC1.


### Parameters ###

1. *Database_Result* `$objRow`

	Database result of the frontend module.
	
2. *string* `$strBuffer`

	The generated frontend module buffer.



### Return Values ###

Return `$strBuffer` or your custom modification.


### Example ###

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


### See Also ###

- [getContentElement](getContentElement.md) – triggered when a content element is generated
- [getArticle](getArticle.md) – tiggered when an article is generated
- [getForm](getForm.md) – triggered when a form is generated

