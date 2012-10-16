getArticle
----------

The `getArticle` allows you to override the configuration of an article prior to rendering. It does not expect a return value.


### Parameters ###

1. *Database_Result* `$objRow`
	
	The database result from table `tl_article`.


### Example ###

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['validateFormField'][] = array('MyClass', 'myGetArticle');

// MyClass.php
public function myGetArticle(Database_Result $objRow)
{
	// Add CSS class based on a custom field
	if ($objRow->grid == '4')
	{
		$arrCSS = deserialize($objRow->cssID, true);
		$arrCSS[1] = trim($arrCSS[1] . ' grid4');
		$objRow->cssID = serialize($arrCSS);
	}
}
```


### See Also ###

- [getFrontendModule](getFrontendModule.md) – triggered when a frontend module is generated
- [getContentElement](getContentElement.md) – triggered when a content element is generated
- [getForm](getForm.md) – triggered when a form is generated

