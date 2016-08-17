# getSearchablePages

The `getSearchablePages` hook is triggered when the the search index is rebuilt.
It passes the array of pages and the ID of the root page as arguments and
expects an array of absolute URLs (!) as return value.

> #### primary:: Available   
> from Contao 2.2.0.


## Parameters

1. *array* `$arrPages`

    List of absolute URLs that should be indexed.

2. *int* `$intRoot`

    ID of the current root page. Prior to Contao 2.11, this can be 0 when no
    root page is added in the page tree. This parameter is not always available.

3. *boolean* `$blnSitemap`

    `true` if the hook is triggered when updating XML sitemap. This parameter is
    not always available.

4. *string* `$strLanguage`

    Language of the generated root page. This parameter is not always available.


## Return Values

Return the list of pages that should be indexed. Be aware that this simply means
these URLs will be requested, and each page is responsible for it's indexing. By
checking `$blnSitemap`, you can decide wether to include your pages in the XML
sitemap or only for the search index.


## Example

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['getSearchablePages'][] = array('MyClass', 'myGetSearchablePages');

// MyClass.php
public function myGetSearchablePages($arrPages, $intRoot=null, $blnSitemap=false, $strLanguage=null)
{
    $arrPages[] = $this->Environment->base . 'custom.html';

    return $arrPages;
}
```


## More information


### References

- [system/modules/core/library/Contao/Automator.php](https://github.com/contao/core/blob/3.5.0/system/modules/core/library/Contao/Automator.php#L405-L412)
- [system/modules/core/classes/RebuildIndex.php](https://github.com/contao/core/blob/3.5.0/system/modules/core/classes/RebuildIndex.php#L73-L80)
