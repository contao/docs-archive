# closeAccount

The `closeAccount` hook is triggered when a user closes his account. It passes
the user ID, the operation mode and the module as arguments and does not expect
a return value.

> **Tag** Available from version 2.8.0.


## Parameters

1. *int* `$intId`

    ID of the user which closed his account.

2. *string* `$strMode`

    The "close account" mode. Either `close_deactivate` or `close_delete`.

3. *object* `$objModule`

    The front end module object. This allows you to retrieve all data from the
    current `tl_module` result set.


## Example

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['closeAccount'][] = array('MyClass', 'myCloseAccount');

// MyClass.php
public function myCloseAccount($intId, $strMode, $objModule)
{
    if ($strMode == 'close_delete')
    {
        // Do something
    }
}
```

## More information


### References

- [system/modules/core/modules/ModuleCloseAccount.php](https://github.com/contao/core/blob/3.5.0/system/modules/core/modules/ModuleCloseAccount.php#L109-L116)


### See also

- [createNewUser](createNewUser.md) - triggered when a new front end user registers on the website.
- [updatePersonalData](updatePersonalData.md) - triggered after a member has updated his personal data.
