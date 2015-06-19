# listComments


The `listComments` hook is triggered when listing comment from unknown source in the back end. It passes the current record as argument and expects a string as return value. It is available from version 2.8.RC2.


### Parameters

1. *array* `$arrRow`

	The current comment record data.


## Return Values 

Return a string representing your comment, or an empty string if your method is not responsible for the source table.


## Example 

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['listComments'][] = array('MyClass', 'myListComments');

// MyClass.php
public function myListComments($arrRow)
{
	if ($arrRow['source'] == 'tl_mytable')
	{
    	return '<a href="contao/main.php?do=...">' . $arrRow['title'] . '</a>';
    }

	return '';
}
```


## More Information


### References

- [system/modules/comments/dca/tl_comments.php](https://github.com/contao/core/blob/2.11.7/system/modules/comments/dca/tl_comments.php#L488)


### See Also

- [addComment](addComment.md) - triggered when a comment is added
- [isAllowedToEditComment](isAllowedToEditComment.md) - triggered to determine permission on a comment in the back end
