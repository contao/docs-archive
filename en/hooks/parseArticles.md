parseArticles
----------------

The `parseArticles` hook allows to manipulate the parsed articles.


### Parameters ###

1. *FrontendTemplate* `$objTemplate`

	...

2. *Database_Result* `$objArticleRow`

	...

3. *ModuleNews* `$objModule`

	...


### Return Values ###

…


### Example ###

```php
<?php

// code example here

// HOOK: add custom logic
if (isset($GLOBALS['TL_HOOKS']['parseArticles']) && is_array($GLOBALS['TL_HOOKS']['parseArticles']))
{
	foreach ($GLOBALS['TL_HOOKS']['parseArticles'] as $callback)
	{
		$this->import($callback[0]);
		$this->$callback[0]->$callback[1]($objTemplate, $objArticles->row(), $this);
	}
}

```


### See Also ###

- [relatedHookOrMethod](relatedHookOrMethod) - triggered when ...
