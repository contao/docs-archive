getRootPageFromUrl
----------------

The `getRootPageFromUrl` hook allows to overwrite the root page.

### Parameters ###



### Return Values ###

*Database_Result* `$objRootPage`


### Example ###

```php
<?php

// code example here

// HOOK: add custom logic
if (isset($GLOBALS['TL_HOOKS']['getRootPageFromUrl']) && is_array($GLOBALS['TL_HOOKS']['getRootPageFromUrl']))
{
	foreach ($GLOBALS['TL_HOOKS']['getRootPageFromUrl'] as $callback)
	{
		$this->import($callback[0]);
		$objRootPage = $this->$callback[0]->$callback[1]();

		if ($objRootPage instanceof Database_Result)
		{
			return $objRootPage;
		}
	}
}

```


### See Also ###

- [relatedHookOrMethod](relatedHookOrMethod) - triggered when ...
