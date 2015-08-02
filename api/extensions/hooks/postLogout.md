# postLogout

The `postLogout` hook is triggered after a user has logged out from the front
end. It passes the user object as argument and does not expect a return value.

> **Tag** Available from version 2.4.3.


## Parameters

1. *FrontendUser* `$objUser`

    The front end user (object) which has been logged out.


## Example

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['postLogout'][] = array('MyClass', 'myPostLogout');

// MyClass.php
public function myPostLogout(FrontendUser $objUser)
{
    // Do something
}
```

## More information


### References

- [system/modules/core/library/Contao/User.php](https://github.com/contao/core/blob/3.5.0/system/modules/core/library/Contao/User.php#L637-L644)


### See also

- [postLogin](postLogin.md) - triggered after a front end user has logged in.
