createNewUser
-------------

The ```createNewUser``` hook is triggered when a new front end user registers on the website. It passes the ID of the new user and the data array as arguments and does not expect a return value. It is available from version 2.2.0.


### Parameters ###

- *int* ```$intId```

	Unique ID of the user

- *array* ```$arrData```

	All values which have been submitted on the registration form. Be aware that the user ID is not contained in this array (```$arrData['id']``` is empty).


### Example ###

```php
// config.php
$GLOBALS['TL_HOOKS']['createNewUser'][] = array('MyClass', 'myCreateNewUser');
 
// MyClass.php
public function myCreateNewUser($intId, $arrData)
{
    // Modify the record
}
``` 


### See Also ###

- [activateAccount](activateAccount.md) - triggered when a new front end account is activated
- [postLogin](postLogin.md) - triggered after a user has logged in
