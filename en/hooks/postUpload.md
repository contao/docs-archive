postUpload
----------

The ```postUpload``` hook is triggered after a user has uploaded one or more file in the back end. It passes an array of filenames as argument and does not expect a return value. It is available from version 2.6.4.


### Example ###

```php
// config.php
$GLOBALS['TL_HOOKS']['postUpload'][] = array('MyClass', 'myPostUpload');
 
// MyClass.php
public function myPostUpload($arrFiles)
{
    // Do something
}
``` 
