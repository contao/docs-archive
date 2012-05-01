importUser
----------

The ```importUser``` hook is triggered when a username cannot be found in the database. It passes the username, the password and the table name as arguments and expects a boolean return value. It is available from version 2.7.RC1.


### Parameters ###

1. *string* ```$strUsername```

	The unknown username

2. *string* ```$strPassword```

	The password submitted in the login form

3. *string* ```$strTable```

	The user model table, either ```tl_member``` (for frontend) or ```tl_user``` (for backend)


### Example ###

```php
// config.php
$GLOBALS['TL_HOOKS']['importUser'][] = array('MyClass', 'myImportUser');
 
// MyClass.php
public function myImportUser($strUsername, $strPassword, $strTable)
{
    if ($strTable == 'tl_member')
    {
        // Import user from an LDAP server
        if ($this->importUserFromLdap($strUsername, $strPassword))
        {
            return true;
        }
    }
 
    return false;
}
``` 


### See Also ###

- [checkCredentials](checkCredentials.md) - triggered when a login attempt fails due to a wrong password
- [postLogin](postLogin.md) - triggered after a user has logged out
- [postLogin](postLogin.md) - triggered after a user has logged in
