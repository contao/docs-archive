importUser
----------

The importUser hook is triggered when a username cannot be found in the database. It passes the username, the password and the table name as arguments and expects a boolean return value. It is available from version 2.7.RC1.

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
