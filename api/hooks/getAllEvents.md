# getAllEvents

The `getAllEvents` hook allows you to modify the result sets of calendar and
event modules. It passes the current result set, the IDs of the parent items
and the start and end time as arguments and expects a result set (array)
as return value.

> **Tag** Available from version 2.6.4.


## Parameters

1. *array* `$arrEvents`

    Associative array of all events (grouped by date).

2. *array* `$arrCalendars`

    The IDs of calendars enabled in the front end module.

3. *int* `$intStart`

    The calendar period start date (e.g. if the user selected "current month",
    it will contain the timestamp of 00:00:00 of the first day of the month).

4. *int* `$intEnd`

    The calendar period end date (e.g. if the user selected "current month",
    it will contain the timestamp of 23:59:59 of the last day of the month).

5. *object* `$objModule`

    The active front end module instance.


## Return Values

Return `$arrEvents` after you did your custom modifications.


## Example

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['getAllEvents'][] = array('MyClass', 'myGetAllEvents');

// MyClass.php
public function myGetAllEvents($arrEvents, $arrCalendars, $intStart, $intEnd, $objModule)
{
    ksort($arrEvents);
    return $arrEvents;
}
```


## More information


### References

- [system/modules/calendar/Events.php](https://github.com/contao/core/blob/2.11.7/system/modules/calendar/Events.php#L195)


### See also

- [parseArticles](parseArticles.md) – triggered when parsing news articles
