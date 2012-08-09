getSystemMessages
----------------

The `getSystemMessages` hook allows to add additional messages to the backend startpage.


### Parameters ###


### Return Values ###

*string* $strBuffer


### Example ###

```php
<?php

// code example here

// HOOK: add custom messages
if (isset($GLOBALS['TL_HOOKS']['getSystemMessages']) && is_array($GLOBALS['TL_HOOKS']['getSystemMessages']))
{
	foreach ($GLOBALS['TL_HOOKS']['getSystemMessages'] as $callback)
	{
		$this->import($callback[0]);
		$strBuffer = $this->$callback[0]->$callback[1]();

		if ($strBuffer != '')
		{
			$arrMessages[] = $strBuffer;
		}
	}
}


```


### See Also ###

- [relatedHookOrMethod](relatedHookOrMethod) - triggered when ...
