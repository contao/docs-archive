# importUser

The `importUser` hook is triggered when a username cannot be found in the
database. It passes the username, the password and the table name as arguments
and expects a boolean return value.

> #### primary:: Available   
> from Contao 2.7.0-RC1.


## Parameters

1. *string* `$strUsername`

    The unknown username.

2. *string* `$strPassword`

    The password submitted in the login form.

3. *string* `$strTable`

    The user model table, either `tl_member` (for front end) or `tl_user`
    (for back end).


## Return Values

A record must exist in the database for Contao to load a user. Return `true` if
you added the user to the respective table, or `false` if not.


## Example

```php
<?php

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


## More information


### References

- [system/modules/core/library/Contao/User.php](https://github.com/contao/core/blob/master/system/modules/core/library/Contao/User.php#L325-L338)


### See also

- [checkCredentials](checkCredentials.md) - triggered when a login attempt fails due to a wrong password.
- [postLogin](postLogin.md) - triggered after a user has logged out.
- [postLogin](postLogin.md) - triggered after a user has logged in.
