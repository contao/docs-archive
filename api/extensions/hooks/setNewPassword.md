# setNewPassword

The `setNewPassword` hook is triggered after a new password has been set. It
passes the user object and the encrypted password as arguments and does not
expect a return value.

> #### primary:: Available   
> from Contao 2.2.3.


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


## More information


### References

- [system/modules/core/modules/ModulePassword.php](https://github.com/contao/core/blob/3.5.0/system/modules/core/modules/ModulePassword.php#L233-L240)
- [system/modules/core/modules/ModuleChangePassword.php](https://github.com/contao/core/blob/3.5.0/system/modules/core/modules/ModuleChangePassword.php#L179-L186)
- [system/modules/core/dca/tl_member.php](https://github.com/contao/core/blob/3.5.0/system/modules/core/dca/tl_member.php#L551-L561)


### See also

- [createNewUser](createNewUser.md) - triggered when a new front end user registers on the website.
- [activateAccount](activateAccount.md) - triggered when a new front end account is activated.
