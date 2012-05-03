loadFormField
-------------

The `loadFormField` hook is triggered when a form field is loaded. It passes the widget object, the form ID and the form data as arguments and expects a widget object as return value. It is available from version 2.5.0.


### Parameters ###

1. *Widget* `$objWidget`

	Object of the current frontend widget. Use this to modify the widget properties prior to rendering.

2. *string* `$strForm`

	Alias of the current form.

3. *array* `$arrForm`

	The form configuration, a tl_form record.


### Example ###

```php
<?php

// config.php
$GLOBALS['TL_HOOKS']['loadFormField'][] = array('MyClass', 'myLoadFormField');

// MyClass.php
public function myLoadFormField(Widget $objWidget, $strForm, $arrForm)
{
    $objWidget->class = 'myclass';
    return $objWidget;
}
```


### See Also ###

- [validateFormField](validateFormField.md) - triggered when a form field is submitted
- [processFormData](processFormData.md) - triggered after a form has been submitted
