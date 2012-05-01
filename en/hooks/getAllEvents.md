getAllEvents
------------

The getAllEvents hook allows you to modify the result sets of calendar and event modules. It passes the current result set, the IDs of the parent items and the start and end time as arguments and expects a result set (array) as return value. It is available from version 2.6.4.

```php
// config.php
$GLOBALS['TL_HOOKS']['getAllEvents'][] = array('MyClass', 'myGetAllEvents');
 
// MyClass.php
public function myGetAllEvents($arrEvents, $arrCalendars, $intStart, $intEnd, Module $objModule)
{
    ksort($arrEvents);
    return $arrEvents;
}
``` 
