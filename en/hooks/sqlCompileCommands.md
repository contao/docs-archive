sqlCompileCommands
----------------

The `sqlCompileCommands` hook allows to manipulate the compile queries.


### Parameters ###

1. *array* `$return`

	Array that contains queries.


### Return Values ###

*array* $return


### Example ###

```php
<?php

// code example here

// HOOK: allow third-party developers to modify the array (see #3281)
if (isset($GLOBALS['TL_HOOKS']['sqlCompileCommands']) && is_array($GLOBALS['TL_HOOKS']['sqlCompileCommands']))
{
	foreach ($GLOBALS['TL_HOOKS']['sqlCompileCommands'] as $callback)
	{
		$this->import($callback[0]);
		$return = $this->$callback[0]->$callback[1]($return);
	}
}

```


### See Also ###

- [relatedHookOrMethod](relatedHookOrMethod) - triggered when ...
