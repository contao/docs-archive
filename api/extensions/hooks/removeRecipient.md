# removeRecipient

The `removeRecipient` hook is triggered when a newsletter recipient is removed.
It passes the email address and the channel IDs as argument and does not expect
a return value.

> #### primary:: Available   
> from Contao 2.8.0-RC1.


## Parameters

1. *string* `$strEmail`

    The recipient's email address which has been removed.

2. *array* `$arrChannels`

    The channels from which the recipient has unsubscribed.


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


## More information


### References

- [system/modules/newsletter/modules/ModuleUnsubscribe.php](https://github.com/contao/core/blob/3.5.0/system/modules/newsletter/modules/ModuleUnsubscribe.php#L193-L200)


### See also

- [activateRecipient](activateRecipient.md) - triggered when a new newsletter recipient is added.
