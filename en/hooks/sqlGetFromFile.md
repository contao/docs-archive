sqlGetFromFile
----------------

The `sqlGetFromFile` hook allows to modify the file-generated DB-array



### Parameters ###

1. *array* `$dbArray`

	Contains the fields for every table



### Return Values ###

*array* $dbArray


### Example ###

```php
<?php

// code example here

// HOOK: allow third-party developers to modify the array (see #3281)
if (isset($GLOBALS['TL_HOOKS']['sqlGetFromFile']) && is_array($GLOBALS['TL_HOOKS']['sqlGetFromFile']))
{
	foreach ($GLOBALS['TL_HOOKS']['sqlGetFromFile'] as $callback)
	{
		$this->import($callback[0]);
		$return = $this->$callback[0]->$callback[1]($return);
	}
}

```


### See Also ###

- [relatedHookOrMethod](relatedHookOrMethod) - triggered when ...
