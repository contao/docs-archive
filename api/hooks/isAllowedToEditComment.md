# isAllowedToEditComment


The `isAllowedToEditComment` hook is triggered to determine permission on a comment from unknown source in the back end. It passes the comment parent ID and source table and expects a boolean return value.


## Parameters 

1. *int* `$intParent`

	The parent record ID.

2. *string* `$strSource`

	The parent table name.


## Return Values 

If you return `true`, access to the comment is granted. Return `false` if access is prohibited or your function is not responsible for this comment.


## Example 

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['isAllowedToEditComment'][] = array('MyClass', 'myIsAllowedToEditComment');

// MyClass.php
public function myIsAllowedToEditComment($intParent, $strSource)
{
	// Check the access to your custom module
	if (BackendUser::getInstance()->hasAccess('custom', 'modules'))
	{
		return true;
	}

	return false;
}
```

## More Information


### References

- [system/modules/comments/dca/tl_comments.php](https://github.com/contao/core/blob/2.11.7/system/modules/comments/dca/tl_comments.php#L406)


### See Also

- [addComment](addComment.md) - triggered when a comment is added
- [listComments](listComments.md) - triggered when comments are listed in the back end
