getUserNavigation
----------------

The `getUserNavigation` hook allows to manipulate the user navigation.


### Parameters ###

1. *array* `$arrModules`

	Array list of modules.

2. *boolean* `$blnShowAll`

	Flag to show all

### Return Values ###

*array* $arrModules


### Example ###

```php
<?php

// code example here


// HOOK: add custom logic
if (isset($GLOBALS['TL_HOOKS']['getUserNavigation']) && is_array($GLOBALS['TL_HOOKS']['getUserNavigation']))
{
	foreach ($GLOBALS['TL_HOOKS']['getUserNavigation'] as $callback)
	{
		$this->import($callback[0]);
		$arrModules = $this->$callback[0]->$callback[1]($arrModules, $blnShowAll);
	}
}

```


### See Also ###

- [relatedHookOrMethod](relatedHookOrMethod) - triggered when ...
