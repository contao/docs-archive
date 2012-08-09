parseTemplate
----------------

The `parseTemplate` hook allows to manipulate the parsed template.


### Parameters ###

1. *Template* `$objTemplate`

	

### Return Values ###

…


### Example ###

```php
<?php

// code example here

// HOOK: add custom parse filters
if (isset($GLOBALS['TL_HOOKS']['parseTemplate']) && is_array($GLOBALS['TL_HOOKS']['parseTemplate']))
{
	foreach ($GLOBALS['TL_HOOKS']['parseTemplate'] as $callback)
	{
		$this->import($callback[0]);
		$this->$callback[0]->$callback[1]($this);
	}
}

```


### See Also ###

- [relatedHookOrMethod](relatedHookOrMethod) - triggered when ...
