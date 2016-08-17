# storeFormData

The `storeFormData` hook is triggered before a submitted form is stored to the
database. It passes the result set and the form object and expects the result
set as return value.

> #### primary:: Available   
> from Contao 2.11.0-rc1.


## Parameters

1. *array* `$arrSet`

    The result set that will be written to the database table.

2. *Form* `$objForm`

    The form instance.


## Return Values

Return `$arrSet` or an array of key => values that should be written to the
database.


## Example

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['storeFormData'][] = array('MyClass', 'myStoreFormData');

// MyClass.php
public function myStoreFormData($arrSet, $objForm)
{
    $arrSet['member'] = 0;

    if (FE_USER_LOGGED_IN && $this->Database->fieldExists('member', $objForm->targetTable))
    {
        // Also store the member ID who submitted the form
        $arrSet['member'] = FrontendUser::getInstance()->id;
    }

    return $arrSet;
}
```


## More information


### References

- [system/modules/core/forms/Form.php](https://github.com/contao/core/blob/3.5.0/system/modules/core/forms/Form.php#L483-L490)


### See also

- [processFormData](processFormData.md) – triggered after a form has been submitted.
- [getForm](getForm.md) – manipulate the generation of the forms.
- [loadFormField](loadFormField.md) – triggered when a form field is loaded.
- [validateFormField](validateFormField.md) – triggered when a form field is submitted.
