getCacheKey
----------------

The `getCacheKey` hook is used to manipulate the cache key.


### Parameters ###

1. *string* `$strCacheKey`

	The request string generated from $this->Environment->base.


### Return Values ###

$strCacheKey


### Example ###

```php
<?php

// code example here

// HOOK: add custom logic
if (isset($GLOBALS['TL_HOOKS']['getCacheKey']) && is_array($GLOBALS['TL_HOOKS']['getCacheKey']))
{
	foreach ($GLOBALS['TL_HOOKS']['getCacheKey'] as $callback)
	{
		$this->import($callback[0]);
		$strCacheKey = $this->$callback[0]->$callback[1]($strCacheKey);
	}
}

```


### See Also ###

- [relatedHookOrMethod](relatedHookOrMethod) - triggered when ...
