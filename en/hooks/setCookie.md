setCookie
----------------

The `setCookie` hook allows to manipulate the previously set cookies.


### Parameters ###

1. *stdClass* `$objCookie`

	Contains cookie-parameters


### Return Values ###

*stdClass* $objCookie


### Example ###

```php
<?php

// code example here

// HOOK: allow to add custom logic
if (isset($GLOBALS['TL_HOOKS']['setCookie']) && is_array($GLOBALS['TL_HOOKS']['setCookie']))
{
	foreach ($GLOBALS['TL_HOOKS']['setCookie'] as $callback)
	{
		$this->import($callback[0], 'objCookie', true);
		$objCookie = $this->objCookie->$callback[1]($objCookie);
	}
}

```


### See Also ###

- [relatedHookOrMethod](relatedHookOrMethod) - triggered when ...
