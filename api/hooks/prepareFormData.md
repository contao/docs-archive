prepareFormData
-------------

The `prepareFormData` hook is triggered after a form has been submitted, but before it is processed. It passes the form data array, the form labels array and the form object as arguments and does not expect a return value. This way the data can be changed or extended, prior to execution of actions like email distribution or data storage. It is available from version 3.0.0.


### Parameters ###

1. *array* `$arrSubmitted`

	The user input from the form.

2. *arrray* `$arrLabels`

	The fields labels of the form.

3. *Form* `$objForm`

	The form module instance.


### Example ###

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['prepareFormData'][] = array('MyClass', 'myPrepareFormData');

// MyClass.php
public function myPrepareFormData(&$arrSubmitted, $arrLabels, $objForm)
{
    // this calculates a deadline from a given timestamp
    // and stores it as deadline in $arrSubmitted 
    $arrSubmitted['deadline'] = $strtotime('+1 hour', $arrSubmitted('tstamp'));
}
```


### References ###

- [system/modules/core/forms/Form.php](https://github.com/contao/core/blob/3.0.0/system/modules/core/forms/Form.php#L257)


### See Also ###

- [storeFormData](storeFormData.md) – triggered after a form has been submitted
- [processFormData](processFormData.md) – triggered after a form has been submitted
- [getForm](getForm.md) – manipulate the generation of the forms
- [loadFormField](loadFormField.md) – triggered when a form field is loaded
- [validateFormField](validateFormField.md) – triggered when a form field is submitted
