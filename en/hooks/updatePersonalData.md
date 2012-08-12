updatePersonalData
----------------

The `updatePersonalData` hook allows to manipulate the personal data of a user.


### Parameters ###

1. *User* `$objUser`

	...

2. *string* `$strValue`

	...

3. *ModulePersonalData* `$objPersonalData`

	...


### Return Values ###



### Example ###

```php
<?php

// code example here

// HOOK: updated personal data
if (isset($GLOBALS['TL_HOOKS']['updatePersonalData']) && is_array($GLOBALS['TL_HOOKS']['updatePersonalData']))
{
	foreach ($GLOBALS['TL_HOOKS']['updatePersonalData'] as $callback)
	{
		$this->import($callback[0]);
		$this->$callback[0]->$callback[1]($this->User, $_SESSION['FORM_DATA'], $this);
	}
}

```


### See Also ###

- [relatedHookOrMethod](relatedHookOrMethod) - triggered when ...
