activateAccount
---------------

The ```activateAccount``` hook is triggered when a new front end account is activated. It passes the user object as argument and does not expect a return value. It is available from version 2.4.3.


### Parameters ###

- *Database_Result* ```$objUser```  

	A database result set of the activated user account


### Example ###

```php
// config.php
$GLOBALS['TL_HOOKS']['activateAccount'][] = array('MyClass', 'myActivateAccount');
 
// MyClass.php
public function myActivateAccount(Database_Result $objUser)
{
    // Do something
}
```


### See Also ###

- [createNewUser](hooks/createNewUser.md) - triggered when a new front end user registers
- [closeAccount](hooks/closeAccount.md) - triggered when a user closes his account
- [postLogin](hooks/postLogin.md) - triggered after a user logged in
- [postLogout](hooks/postLogout.md) - triggered after a user logged out