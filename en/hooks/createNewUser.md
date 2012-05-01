createNewUser
-------------

The createNewUser hook is triggered when a new front end user registers on the website. It passes the ID of the new user and the data array as arguments and does not expect a return value. It is available from version 2.2.0.

```php
// config.php
$GLOBALS['TL_HOOKS']['createNewUser'][] = array('MyClass', 'myCreateNewUser');
 
// MyClass.php
public function myCreateNewUser($intId, $arrData)
{
    // Modify the record
}
``` 
