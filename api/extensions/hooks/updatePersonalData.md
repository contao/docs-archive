# updatePersonalData

The `updatePersonalData` hook is triggered after a member has updated his
personal data. It passes the front end user, the updated data and the front
end module and does not expect a return value.

Be aware that the front end user object and the database has already been
updated when this hook is triggered.


## Parameters

1. *FrontendUser* `$objUser`

    The front end user instance who changed his data.

2. *array* `$arrData`

    The submitted form data.

3. *Module* `$objModule`

    The front end module of type `ModulePersonalData`.


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


## More information


### References

- [system/modules/core/modules/ModulePersonalData.php](https://github.com/contao/core/blob/3.5.0/system/modules/core/modules/ModulePersonalData.php#L334-L341)


### See also

- [createNewUser](createNewUser.md) – triggered when a new front end user registers on the website.
- [activateAccount](activateAccount.md) - triggered when a new front end account is activated.
