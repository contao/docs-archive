# activateAccount

The `activateAccount` hook is triggered when a new front end account is activated.

> **Tag** Available from version 2.4.3.


## Parameters

1. *MemberModel* `$memberModel`

    A model of the activated user account.
    
2. *object* `$registrationModule`

    The registration module that was used to activate the account.


## Example

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['activateAccount'][] = array('MyClass', 'myActivateAccount');

// MyClass.php
public function myActivateAccount(MemberModel $memberModel, ModuleRegistration $registrationModule)
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
