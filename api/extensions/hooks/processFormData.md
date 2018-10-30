# processFormData

The `processFormData` hook is triggered after a form has been submitted. It
passes the form data array, the Data Container Array and the files array as
arguments and does not expect a return value.

> #### primary:: Available   
> from Contao 2.4.4.


## Parameters

1. *array* `$arrPost`

    Form data submitted by the visitor.

2. *array* `$arrForm`

    The form configuration from `tl_form` table.

3. *array* `$arrFiles`

    Contains information about uploaded files (from "upload" widgets).

4. *array* `$arrLabels`
    
    The field labels of the form.

5. *form* $objForm

    The form instance.
 

## Example

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['processFormData'][] = array('MyClass', 'myProcessFormData');

// MyClass.php
public function myProcessFormData($arrPost, $arrForm, $arrFiles, $arrLabels, $objForm)
{
    // Do something
}
```

## More information


### References

- [system/modules/core/forms/Form.php](https://github.com/contao/core/blob/3.5.0/system/modules/core/forms/Form.php#L514-L521)


### See also

- [prepareFormData](prepareFormData.md) - triggered after a form has been submitted, but before it is processed
- [storeFormData](storeFormData.md) - triggered before a submitted form is stored to the database.
- [loadFormField](loadFormField.md) - triggered when a form field is loaded.
- [validateFormField](validateFormField.md) - triggered when a form field is submitted.
