listComments
------------

The `listComments` hook is triggered when comments are listed in the back end. It passes the current record as argument and expects a string as return value. It is available from version 2.8.RC2.


### Parameters

1. *array* `$arrRow`

	The current comment record data.


### Example ###

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['listComments'][] = array('MyClass', 'myListComments');

// MyClass.php
public function myListComments($arrRow)
{
    return '<a href="contao/main.php?do= … ">' . $arrRow['title'] . '</a>';
}
```


### See Also ###

- [addComment](addComment.md) - triggered when a comment is added
- [isAllowedToEditComment](isAllowedToEditComment.md) - triggered to determine permission on a comment in the back end
