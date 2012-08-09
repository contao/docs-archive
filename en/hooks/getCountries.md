getCountries
----------------

The `getCountries` hook allows to add or remove certain countries.


### Parameters ###

1. *array* `$countries`


### Return Values ###

$countries array


### Example ###

```php
<?php

// code example here

// HOOK: add custom logic
if (isset($GLOBALS['TL_HOOKS']['getCountries']) && is_array($GLOBALS['TL_HOOKS']['getCountries']))
{
	foreach ($GLOBALS['TL_HOOKS']['getCountries'] as $callback)
	{
		$this->import($callback[0]);
		$return = $this->$callback[0]->$callback[1]($return);
	}
}
		
```


### See Also ###

- [relatedHookOrMethod](relatedHookOrMethod) - triggered when ...
