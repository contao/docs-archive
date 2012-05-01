addComment
----------

The ```addComment``` hook is triggered when a comment is added. It passes the ID of the record and the data array as arguments and does not expect a return value. It is available from version 2.8.2.


### Example ###

```php
// config.php
$GLOBALS['TL_HOOKS']['addComment'][] = array('MyClass', 'myAddComment');
 
// MyClass.php
public function myAddComment($intId, $arrSet)
{
    // Do something
}
``` 
