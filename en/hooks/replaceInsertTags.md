replaceInsertTags
-----------------

The replaceInsertTags hook is triggered when an unknown insert tag is found. It passes the insert tag as argument and expects the replacement value or false as return value. It is available from version 2.6.0.

```php
// config.php
$GLOBALS['TL_HOOKS']['replaceInsertTags'][] = array('MyClass', 'myReplaceInsertTags');
 
// MyClass.php
public function myReplaceInsertTags($strTag)
{
    if ($strTag == 'mytag')
    {
        return 'mytag replacement';
    }
 
    return false;
}
``` 
