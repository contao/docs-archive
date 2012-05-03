getSearchablePages
------------------

The `getSearchablePages` hook is triggered when the the search index is rebuilt. It passes the array of pages and the ID of the root page as arguments and expects an array of absolute URLs (!) as return value. It is available from version 2.2.0.


### Parameters ###

1. *array* `$arrPages`

	List of absolute URLs that should be indexed.

2. *int* `$intRoot`

	ID of the current root page. Prior to Contao 2.11, this can be 0 when no root page is added in the page tree.


### Example ###

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['getSearchablePages'][] = array('MyClass', 'myGetSearchablePages');

// MyClass.php
public function myGetSearchablePages($arrPages, $intRoot)
{
    return array_merge($arrPages, array('Additional pages'));
}
```
