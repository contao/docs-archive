addLogEntry
-----------

The addLogEntry hook is triggered when a new log entry is added. It passes the message, the function and the action as arguments and does not expect a return value. It is available from version 2.8.RC1.

```php
// config.php
$GLOBALS['TL_HOOKS']['addLogEntry'][] = array('MyClass', 'myAddLogEntry');
 
// MyClass.php
public function myAddLogEntry($strText, $strFunction, $strAction)
{
    // Do something
}
``` 
