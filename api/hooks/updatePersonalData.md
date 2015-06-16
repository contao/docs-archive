# updatePersonalData


The `updatePersonalData` hook is triggered after a member has updated his personal data. It passes the frontend user, the updated data and the frontend module and does not expect a return value.

Be aware that the frontend user object and the database has already been updated when this hook is triggered.


## Parameters 

1. *FrontendUser* `$objUser`

	The frontend user instance who changed his data.

2. *array* `$arrData`

	The submitted form data.

3. *Module* `$objModule`

	The frontend module of type `ModulePersonalData`.


## Example 

```php
<?php
// config.php
$GLOBALS['TL_HOOKS']['updatePersonalData'][] = array('MyClass', 'myUpdatePersonalData');

// MyClass.php
public function myUpdatePersonalData($objUser, $arrData, $objModule)
{
	// Do something
}
```


## More Information


### References

- [system/modules/frontend/ModulePersonalData.php](https://github.com/contao/core/blob/2.11.7/system/modules/frontend/ModulePersonalData.php#L254)


### See Also

- [createNewUser](createNewUser.md) – triggered when a new front end user registers on the website
- [activateAccount](activateAccount.md) - triggered when a new front end account is activated
