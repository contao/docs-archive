# compileFormFields

The `compileFormFields` hook is triggered when the fields of a form are compiled.
It passes the form fields, the ID of the form and the form object as arguments
and expects the modified form fields as return value.

> #### tag:: Version Information 
> Available from Contao version 3.2.0.


## Parameters

1. *array* `$arrFields`

	An array of `FormFieldModel` instances.

2. *string* `$strFormId`

	Used in the `value` attribute of the hidden form field `FORM_SUBMIT`. Don't confuse with `$objForm->id`.

3. *object* `$objForm`

	The form (an instance of `Contao\Form`).


## Return Values 

The return value should be the `$arrFields` array modified to your needs.
 

## Example

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['compileFormFields'][] = array('MyClass', 'myCompileFormFields');

// MyClass.php
public function myCompileFormFields($arrFields, $intFormId, $objForm)
{
    // modify $arrFields as needed

    return $arrFields;
}
```

## More Information


### References

- [system/modules/core/forms/Form.php](https://github.com/contao/core/blob/support/3.2/system/modules/core/forms/Form.php#L98)
