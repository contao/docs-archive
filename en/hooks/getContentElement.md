getContentElement
-----------------

The `getContentElement` hook is triggered when a content element is rendered. It passes the database object and the buffer string as arguments and expects a buffer string as return value. It is available from version 2.9.0.


### Parameters ###

1. *Database_Result* `$objElement`

	Database result set from table `tl_content`.

2. *string* `$strBuffer`

	The output buffer of the generated content element.


### Return Values ###

You can modify the output buffer (e.g. add a wrapper div) or change the database result and re-generate the content element.


### Examples ###

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['getContentElement'][] = array('MyClass', 'myGetContentElement');

// MyClass.php
public function myGetContentElement(Database_Result $objElement, $strBuffer)
{
    return '<div class="content-element">' . $strBuffer . '</div>';
}
```


### See Also ###

- [getArticle](getArticle.md) – tiggered when an article is generated
- [getFrontendModule](getFrontendModule.md) – triggered when a frontend module is generated
- [getForm](getForm.md) – triggered when a form is generated

