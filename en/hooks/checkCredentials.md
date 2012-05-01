checkCredentials
----------------

The ```checkCredentials``` hook is triggered when a login attempt fails due to a wrong password. It passes the username and password as well as the user object as arguments and expects a boolean return value. It is available from version 2.6.0.


### Parameters ###

- *string* ```$strUsername```

	The username submitted from the login form.

- *string* ```$strPassword```

	The password submitted from the login form.

- *User* ```$objUser```

	User object model from database record with the given username.


### Return Values ###

<span class="undocumented">Please add documentation about return values.</span>


### Example ###

```php
// config.php
$GLOBALS['TL_HOOKS']['checkCredentials'][] = array('MyClass', 'myCheckCredentials');

// MyClass.php
public function myCheckCredentials($strUsername, $strPassword, User $objUser)
{
    // Check against a global database
    if ($this->checkGlobalDbFor($strUsername, $strPassword))
    {
        return true;
    }
 
    return false;
}
``` 


### See Also ###

- [importUser](importUser.md) - triggered when username cannot be found in the database
- [postLogin](postLogin.md) - triggered after a user has logged in
- [postLogout](postLogout.md) - triggered after a user has logged out
