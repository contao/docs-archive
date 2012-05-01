removeOldFeeds
--------------

The ```removeOldFeeds``` hook is triggered when old XML files are being removed from the Contao directory. It does not pass an argument and expects an array of file names to preserve as return value. It is available from version 2.5.8.


### Example ###

```php
// config.php
$GLOBALS['TL_HOOKS']['removeOldFeeds'][] = array('MyClass', 'myRemoveOldFeeds');
 
// MyClass.php
public function myRemoveOldFeeds()
{
    return array('custom.xml');
}
``` 
