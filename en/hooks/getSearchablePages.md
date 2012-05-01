getSearchablePages
------------------

The ```getSearchablePages``` hook is triggered when the the search index is rebuilt. It passes the array of pages and the ID of the root page as arguments and expects an array of absolute URLs (!) as return value. It is available from version 2.2.0.


### Example ###

```php
// config.php
$GLOBALS['TL_HOOKS']['getSearchablePages'][] = array('MyClass', 'myGetSearchablePages');
 
// MyClass.php
public function myGetSearchablePages($arrPages, $intRoot)
{
    return array_merge($arrPages, array('Additional pages'));
}
``` 
