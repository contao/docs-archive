activateAccount
---------------

The `activateAccount` hook is triggered when a new front end account is activated. It passes the user object as argument and does not expect a return value. It is available from version 2.4.3.


### Parameters ###

1. *Database_Result* `$objUser`

	A database result set of the activated user account


### Example ###

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['activateAccount'][] = array('MyClass', 'myActivateAccount');

// MyClass.php
/**
 * @param  Database_Result    $objUser         The database result object
 * @param  ModuleRegistration $objRegistration The registration module
 * @return void                                No return value expected
 */
public function myActivateAccount(Database_Result $objUser, ModuleRegistration $objRegistration)
{
    // Do something
}
```


### References ###

- [system/modules/registration/ModuleRegistration.php](https://github.com/contao/core/blob/2.11.7/system/modules/registration/ModuleRegistration.php#L496)


### See Also ###

- [createNewUser](createNewUser.md) - triggered when a new front end user registers
- [closeAccount](closeAccount.md) - triggered when a user closes his account
- [postLogin](postLogin.md) - triggered after a user logged in
- [postLogout](postLogout.md) - triggered after a user logged out
