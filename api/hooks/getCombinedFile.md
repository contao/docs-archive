# getCombinedFile


The `getCombinedFile` hook is triggered when combining CSS or Javascript files. It passes the file content, a unique key for the temporary file and the mode and expects the content as return value.


## Parameters 

1. *string* `$strContent`

	Content of the file which will be added to the combiner.

2. *string* `$strKey`

	A unique key that represents the current combiner. A file with this name will be stored in `system/scripts/`.

3. *string* `$strMode`

	The combiner mode (constant), either `Combiner::CSS` or `Combiner::JS`


## Return Values 

Return the file content after your modification.


## Example 

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['getCombinedFile'][] = array('MyClass', 'myGetCombinedFile');

// MyClass.php
public function myGetCombinedFile($strContent, $strKey, $strMode)
{
	// Do something

	return $strContent
}
```


## More Information


### References

