getCombinedFile
----------------

The `getCombinedFile` hook is used to manipulate the file combination.


### Parameters ###

1. *string* `$content`

	Filepath of the current file.

2. *string* `$strKey`

	Unique 12-character file-key.
	
3. *string* `$strMode`

	String value of operation mode.


### Return Values ###

File content

### Example ###

```php
<?php

// code example here
// HOOK: modify the file content
if (isset($GLOBALS['TL_HOOKS']['getCombinedFile']) && is_array($GLOBALS['TL_HOOKS']['getCombinedFile']))
{
	foreach ($GLOBALS['TL_HOOKS']['getCombinedFile'] as $callback)
	{
		$this->import($callback[0]);
		$content = $this->$callback[0]->$callback[1]($content, $strKey, $this->strMode);
	}
}
			
```


### See Also ###

- [relatedHookOrMethod](relatedHookOrMethod) - triggered when ...
