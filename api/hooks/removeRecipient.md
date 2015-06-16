# removeRecipient


The `removeRecipient` hook is triggered when a newsletter recipient is removed. It passes the email address and the channel IDs as argument and does not expect a return value. It is available from version 2.8.RC1.


## Parameters 

1. *string* `$strEmail`

	The recipient's email address which has been removed

2. *array* `$arrChannels`

	The channels from which the recipient has unsubscribed


## Example 

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['removeRecipient'][] = array('MyClass', 'myRemoveRecipient');

// MyClass.php
public function myRemoveRecipient($strEmail, $arrChannels)
{
    // Do something
}
```


## More Information


### References

- [system/modules/newsletter/ModuleUnsubscribe.php](https://github.com/contao/core/blob/2.11.7/system/modules/newsletter/ModuleUnsubscribe.php#L197)


### See Also

