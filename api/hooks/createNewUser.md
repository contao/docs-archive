# createNewUser

The `createNewUser` hook is triggered when a new front end user registers on the
website. It passes the ID of the new user and the data array as arguments and does
not expect a return value.

> **Tag** Available from version 2.2.0.


## Parameters

1. *int* `$intId`

    Unique ID of the user

2. *array* `$arrData`

    All values which have been submitted on the registration form. Be aware that
    the user ID is not contained in this array (`$arrData['id']` is empty).


## Example

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['createNewUser'][] = array('MyClass', 'myCreateNewUser');

// MyClass.php
public function myCreateNewUser($intId, $arrData)
{
    // Do something
}
```


## More information


### References

- [system/modules/registration/ModuleRegistration.php](https://github.com/contao/core/blob/2.11.7/system/modules/registration/ModuleRegistration.php#L451)


### See also

- [activateAccount](activateAccount.md) – triggered when a new front end account is activated
- [updatePersonalData](updatePersonalData.md) – triggered after a member has updated his personal data
- [postLogin](postLogin.md) – triggered after a user has logged in
