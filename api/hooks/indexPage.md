# indexPage

The `indexPage` hook is triggered when a page's content is added to the search index.
It passes the content, the data and the data collected for indexing so far as arguments 
and does not expect a return value.
It is available from version 3.0.0.


## Parameters

1. *string* `$strContent`

	The content of the page.

2. *array* `$arrData`

	The data array

3. *array* `$arrSet`

	An array containing the data collected so far.


## Example

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['indexPage'][] = array('MyClass', 'myIndexPage');

// MyClass.php
public function myIndexPage($strContent, $arrData, $arrSet)
{
    // modify $arrSet which will eventually be stored in tl_search

}
```


## More Information


### References

- [system/modules/core/library/Contao/Search.php](https://github.com/contao/core/blob/support/3.2/system/modules/core/library/Contao/Search.php#L131)
