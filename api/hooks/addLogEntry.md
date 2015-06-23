# addLogEntry


The `addLogEntry` hook is triggered when a new log entry is added. It passes the message, the function and the action as arguments and does not expect a return value. It is available from version 2.8.RC1.


## Parameters 

1. *string* `$strText`

	The log message.

2. *string* `$strFunction`

	The PHP source method. Be aware that this is not necessarily a real function, the function accepts any string!

3. *string* `$strAction`

	The log action. Usually one of the following constants (see system/constants.php), but can be any string.
	- TL_ERROR
	- TL_ACCESS
	- TL_GENERAL
	- TL_FILES
	- TL_CRON
	- TL_FORMS
	- TL_CONFIGURATION
	- TL_NEWSLETTER
	- TL_REPOSITORY


## Example 

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['addLogEntry'][] = array('MyClass', 'myAddLogEntry');

// MyClass.php
public function myAddLogEntry($strText, $strFunction, $strAction)
{
    // Do something
}
```


## More Information


### References

- [system/libraries/System.php](https://github.com/contao/core/blob/2.11.7/system/libraries/System.php#L207)
