setNewPassword
--------------

The `setNewPassword` hook is triggered after a new password has been set. It passes the user object and the encrypted password as arguments and does not expect a return value. It is available from version 2.2.3.


### Example ###

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['setNewPassword'][] = array('MyClass', 'mySetNewPassword');

// MyClass.php
public function mySetNewPassword($objUser, $strPassword)
{
    // Do something
}
```
