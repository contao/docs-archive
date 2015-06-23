# setNewPassword


The `setNewPassword` hook is triggered after a new password has been set. It passes the user object and the encrypted password as arguments and does not expect a return value. It is available from version 2.2.3.


## Parameters 

1. *object* `$objUser`

	Current FrontendUser that changed her password.

2. *string* `$strPassword`

	The new password (not encrypted!).


## Example 

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


## More Information


### References

- [system/modules/frontend/ModulePersonalData.php](https://github.com/contao/core/blob/2.11.7/system/modules/frontend/ModulePersonalData.php#L224)
- [system/modules/registration/ModulePassword.php](https://github.com/contao/core/blob/2.11.7/system/modules/registration/ModulePassword.php#L240)
- [system/modules/backend/dca/tl_member.php](https://github.com/contao/core/blob/2.11.7/system/modules/backend/dca/tl_member.php#L424)


### See Also

- [createNewUser](createNewUser.md) - triggered when a new front end user registers on the website
- [activateAccount](activateAccount.md) - triggered when a new front end account is activated
