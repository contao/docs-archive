postLogout
----------

The `postLogout` hook is triggered after a user has logged out from the front end. It passes the user object as argument and does not expect a return value. It is available from version 2.4.3.


### Parameters ###

1. *FrontendUser* `$objUser`

	The frontend user (object) which has been logged out


### Example ###

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

### See Also ###

- [postLogin](postLogin.md) - triggered after a frontend user has logged in
