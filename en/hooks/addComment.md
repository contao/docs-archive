addComment
----------

The `addComment` hook is triggered when a comment is added. It passes the ID of the record and the data array as arguments and does not expect a return value. It is available from version 2.8.2.


### Parameters ###

1. *int* `$intId`

	ID of the new comment database record (Table `tl_comment`)

2. *array* `$arrSet`

	Data of the new comment record (not including the ID).


### Example ###

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['addComment'][] = array('MyClass', 'myAddComment');

// MyClass.php
public function myAddComment($intId, $arrSet)
{
    // Do something
}
```


### See Also ###

- [listComment](listComments.md) - triggered when comments are listed in the back end
- [isAllowedToEditComment](isAllowedToEditComment.md) - triggered to determine permission on a comment in the back end
