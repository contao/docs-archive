validateFormField
-----------------

The `validateFormField` hook is triggered when a form field is submitted. It passes the widget object and the form ID as arguments and expects a widget object as return value. It is available from version 2.5.0.


### Parameters ###

1. *Widget* `$objWidget`

	Object of the current frontend widget. Use it to access form field properties.

2. *int* `$intId`

	ID of the tl\_form\_field record.

3. *array* $arrForm

	Form configuration data from table `tl_form`.

### Return Value ###

Return the `$objWidget` instance after modification or your custom widget.


### Example ###

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['validateFormField'][] = array('MyClass', 'myValidateFormField');

// MyClass.php
public function myValidateFormField(Widget $objWidget, $intId, $arrForm)
{
    if ($objWidget instanceof FormPassword)
    {
        // Do something
    }

    return $objWidget;
}
```


### See Also ###

- [loadFormField](loadFormField.md) - triggered when a form field is loaded
- [processFormData](processFormData.md) - triggered after a form has been submitted
