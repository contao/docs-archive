getForm
----------------

The `getForm` allows to manipulate the generation of the forms.


### Parameters ###

1. *Object* `$objRow`

	Database-row object
	
2. *string* `$strBuffer`

	Generated string.



### Return Values ###

*string* $strBuffer


### Example ###

```php
<?php

// code example here

// HOOK: add custom logic
if (isset($GLOBALS['TL_HOOKS']['getForm']) && is_array($GLOBALS['TL_HOOKS']['getForm']))
{
	foreach ($GLOBALS['TL_HOOKS']['getForm'] as $callback)
	{
		$this->import($callback[0]);
		$strBuffer = $this->$callback[0]->$callback[1]($objRow, $strBuffer);
	}
}

```


### See Also ###

- [relatedHookOrMethod](relatedHookOrMethod) - triggered when ...
