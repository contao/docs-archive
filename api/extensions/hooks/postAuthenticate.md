# postAuthenticate

The `postAuthenticate` hook is triggered after a user was authenticated. It 
passes the user object as argument and does not expect a return value.

> #### primary:: Available   
> from Contao 3.5.0.


## Parameters

1. *User* `$objUser`

    The user (object) which just has been authenticated.


## Example

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['postAuthenticate'][] = array('MyClass', 'mypostAuthenticate');

// MyClass.php
public function mypostAuthenticate(User $objUser)
{
    // Do something
}
```

## More information


### References

- [system/modules/core/library/Contao/User.php](https://github.com/contao/core/blob/3.5.0/system/modules/core/library/Contao/User.php#L291-L298)


### See also

- [postLogin](postLogin.md) - triggered after a front end user has logged in.
- [postLogout](postLogout.md) - triggered after a front end user has logged out.
- [contao/core#5864](https://github.com/contao/core/issues/5864)