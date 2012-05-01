removeRecipient
---------------

The ```removeRecipient``` hook is triggered when a newsletter recipient is removed. It passes the e-mail address and the channel IDs as argument and does not expect a return value. It is available from version 2.8.RC1.


### Parameters ###

- *string* ```$strEmail```

	the recipient's email address which has been removed

- *array* ```$arrChannels```

	the channels from which the recipient has unsubscribed


### Example ###

```php
// config.php
$GLOBALS['TL_HOOKS']['removeRecipient'][] = array('MyClass', 'myRemoveRecipient');
 
// MyClass.php
public function myRemoveRecipient($strEmail, $arrChannels)
{
    // Do something
}
``` 


### See Also ###

- [activateRecipient](hooks/activateRecipient.md) - triggered when a new newsletter recipient is added
