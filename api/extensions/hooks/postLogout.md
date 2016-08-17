# postLogout

The `postLogout` hook is triggered after a user has logged out from the back end 
or front end. It passes the user object as argument and does not expect a return value.

> #### primary:: Available   
> from Contao 2.4.3.


## Parameters

1. *User* `$user`

    The back end or front end user (object) which has been logged out.


## Example

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['postLogout'][] = array('MyClass', 'myPostLogout');

// MyClass.php
public function myPostLogout(User $user)
{
    if ($user instanceof FrontendUser) {
        // Do something with the front end user $user   
    }
}
```

## More information


### References

- [system/modules/core/library/Contao/User.php](https://github.com/contao/core/blob/3.5.0/system/modules/core/library/Contao/User.php#L637-L644)


### See also

- [postLogin](postLogin.md) - triggered after a front end user has logged in.
