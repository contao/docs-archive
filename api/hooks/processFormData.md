# processFormData

The `processFormData` hook is triggered after a form has been submitted. It
passes the form data array, the Data Container Array and the files array as
arguments and does not expect a return value.

> **Tag** Available from version 2.4.4.


## Parameters

1. *array* `$arrPost`

    Form data submitted by the visitor.

2. *array* `$arrForm`

    The form configuration from `tl_form` table.

3. *array* `$arrFiles`

    Contains information about uploaded files (from "upload" widgets).


## Example

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['processFormData'][] = array('MyClass', 'myProcessFormData');

// MyClass.php
public function myProcessFormData($arrPost, $arrForm, $arrFiles)
{
    // Do something
}
```

## More information


### References

- [system/modules/core/forms/Form.php](https://github.com/contao/core/blob/3.5.0/system/modules/core/forms/Form.php#L514-L521)


### See also

- [storeFormData](storeFormData.md) - triggered before a submitted form is stored to the database.
- [loadFormField](loadFormField.md) - triggered when a form field is loaded.
- [validateFormField](validateFormField.md) - triggered when a form field is submitted.
