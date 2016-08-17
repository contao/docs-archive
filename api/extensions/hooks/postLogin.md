# postLogin

The `postLogin` hook is triggered after a user has logged in. This can 
be either in the back end or the front end. It passes the user object 
as argument and does not expect a return value.

> #### primary:: Available   
> from Contao 2.4.3.


## Parameters

1. *User* `$user`

    The back end or front end user (object) which has been logged in.


## Example

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['postLogin'][] = array('MyClass', 'myPostLogin');

// MyClass.php
public function myPostLogin(User $user)
{
    if ($user instanceof FrontendUser) {
        // Do something with the front end user $user  
    }
}
```


## More information


### References

- [system/modules/core/library/Contao/User.php](https://github.com/contao/core/blob/3.5.0/system/modules/core/library/Contao/User.php#L445-L452)


### See also

- [postLogout](postLogout.md) - triggered when a user is logged out.
