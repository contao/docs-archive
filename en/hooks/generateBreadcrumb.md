generateBreadcrumb
----------------

The `generateBreadcrumb` hook is used to manipulate the breadcrumb.


### Parameters ###

1. *array* `$items`

	An array of items.

2. *Object* `$objModule`

	Object of the type ModuleBreadcrumb.


### Return Values ###
*array* $items


### Example ###

```php
<?php

// code example here
// HOOK: add custom logic
if (isset($GLOBALS['TL_HOOKS']['generateBreadcrumb']) && is_array($GLOBALS['TL_HOOKS']['generateBreadcrumb']))
{
	foreach ($GLOBALS['TL_HOOKS']['generateBreadcrumb'] as $callback)
	{
		$this->import($callback[0]);
		$items = $this->$callback[0]->$callback[1]($items, $this);
	}
}


```


### See Also ###

- [relatedHookOrMethod](relatedHookOrMethod) - triggered when ...
