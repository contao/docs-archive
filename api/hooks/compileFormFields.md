# compileFormFields

The `compileFormFields` hook is triggered when the fields of a form are compiled.
It passes the form fields, the ID of the form and the form object as arguments
and expects the modified form fields as return value.
It is available from version 3.2.0.


## Parameters

1. *array* `$arrFields`

	An array of FormField's

2. *int* `$intFormId`

	ID of the form containing the form field which is used for storing form related data in the session.
	Don't confuse with `$objForm->id`.

3. *object* `$objForm`

	The form module instance.


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
