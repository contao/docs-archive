storeFormData
----------------

The `storeFormData` hook allows to manipulate the processed form data.


### Parameters ###

1. *array* `$arrSet`

	...

2. *Form* `$objForm`

	...


### Return Values ###

*array* $arrSet


### Example ###

```php
<?php

// code example here

// HOOK: store form data callback
if (isset($GLOBALS['TL_HOOKS']['storeFormData']) && is_array($GLOBALS['TL_HOOKS']['storeFormData']))
{
	foreach ($GLOBALS['TL_HOOKS']['storeFormData'] as $callback)
	{
		$this->import($callback[0]);
		$arrSet = $this->$callback[0]->$callback[1]($arrSet, $this);
	}
}

```


### See Also ###

- [relatedHookOrMethod](relatedHookOrMethod) - triggered when ...
