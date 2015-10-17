# activateAccount

The `activateAccount` hook is triggered when a new front end account is activated.
It passes the user object as argument and does not expect a return value.

> **Tag** Available from version 2.4.3.


## Parameters

1. *Database_Result* `$objUser`

    A database result set of the activated user account.
    
2. *object* `$objRegistration`

    The registration module that was used to activate the account.


## Example

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


## More information


### References

- [system/modules/core/modules/ModuleRegistration.php](https://github.com/contao/core/blob/3.5.0/system/modules/core/modules/ModuleRegistration.php#L499-L506)


### See also

- [createNewUser](createNewUser.md) - triggered when a new front end user registers.
- [closeAccount](closeAccount.md) - triggered when a user closes his account.
- [postLogin](postLogin.md) - triggered after a user logged in.
- [postLogout](postLogout.md) - triggered after a user logged out.
