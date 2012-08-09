getArticle
----------------

The `getArticle` hook is used to generate additional articles.


### Parameters ###

1. *Object* `$objRow`
	
	Database result object.

### Return Values ###



### Example ###

```php
<?php

// code example here

// HOOK: add custom logic
if (isset($GLOBALS['TL_HOOKS']['getArticle']) && is_array($GLOBALS['TL_HOOKS']['getArticle']))
{
	foreach ($GLOBALS['TL_HOOKS']['getArticle'] as $callback)
	{
		$this->import($callback[0]);
		$this->$callback[0]->$callback[1]($objRow);
	}
}

```


### See Also ###

- [relatedHookOrMethod](relatedHookOrMethod) - triggered when ...
