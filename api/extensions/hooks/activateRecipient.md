# activateRecipient

The `activateRecipient` hook is triggered when a new newsletter recipient is added.
It passes the e-mail address, the recipient IDs and the channel IDs as argument
and does not expect a return value.

> **Tag** Available from version 2.8.0-RC1.


## Parameters

1. *string* `$strEmail`

    The newsletter recipient's email address.

2. *array* `$arrRecipients`

    <span class="undocumented">please add a description for this parameter</span>

3. *array* `$arrChannels`

    <span class="undocumented">please add a description for this parameter</span>


## Example

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['activateRecipient'][] = array('MyClass', 'myActivateRecipient');

// MyClass.php
public function myActivateRecipient($strEmail, $arrRecipients, $arrChannels)
{
    // Do something
}
```


## More information


### References

- [system/modules/newsletter/modules/ModuleSubscribe.php](https://github.com/contao/core/blob/3.5.0/system/modules/newsletter/modules/ModuleSubscribe.php#L183-L190)


### See also

- [removeRecipient](removeRecipient.md) - triggered when a newsletter recipient is removed.
