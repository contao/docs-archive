# activateRecipient


The `activateRecipient` hook is triggered when a new newsletter recipient is added. It passes the e-mail address, the recipient IDs and the channel IDs as argument and does not expect a return value. It is available from version 2.8.RC1.


## Parameters 

1. *string* `$strEmail`

	the newsletter recipient's email address

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


## More Information


### References

- [system/modules/newsletter/ModuleSubscribe.php](https://github.com/contao/core/blob/2.11.7/system/modules/newsletter/ModuleSubscribe.php#L177)


### See Also

